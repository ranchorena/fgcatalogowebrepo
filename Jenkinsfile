pipeline {
    agent any
  
    stages {
        stage('Checkout') {
            steps {
                dir('C:\\Code\\FiberGIS_CatalogoWeb\\CatalogoWeb') {
                    git branch: 'Catalogo2', url: 'https://x-token-auth:ATCTT3xFfGN06AZe4MFMPf8fN8H4LC0_yZb8vtED9eewtRsKS4x1rsitvD1nlzCTNdPXpkufArUfYZPSspjZyauF4jKGM1EqR4L_AmmH9ObmWAJzSzJR7ocVuak2SqxF7AYawIQGnnjBWjJnduwE1o4uHUerliAJYEBSiDP-tJpLWYu8vLRmWvQ=558B95DF@bitbucket.org/geosystems_ar/fgcatalogofront.git'
                    script {
                        def commit_hash = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
                        def commit_message = sh(returnStdout: true, script: 'git log -1 --pretty=%B').trim()
                        env.LAST_COMMIT_HASH = commit_hash
                        env.LAST_COMMIT_MESSAGE = commit_message
                    }                         
                }
            }
        }
        stage('Build') {
            steps {
                dir('C:\\Code\\FiberGIS_CatalogoWeb\\CatalogoWeb') {
                    // Instalar las dependencias de la aplicación utilizando npm
                    bat 'npm install'
                    // Realizar el build de la aplicación sobrescribiendo el baseHref del angular.json
                    bat 'npm run build -- --configuration production --base-href=""'
                    // Realizar el build de la aplicación utilizando el comando npm run build:component
                    //bat 'npm run build:component'
                }
            }
        }    
        stage('SonarQube Analysis') {
            steps {
                dir('C:\\Code\\FiberGIS_CatalogoWeb\\CatalogoWeb') {
                    withSonarQubeEnv('sonarqubeserver') {
                        script {
                            def scannerHome = tool 'sonarscanner'
                            withSonarQubeEnv(credentialsId: 'sonarqube') {
                                bat "${scannerHome}\\bin\\sonar-scanner.bat -Dsonar.projectKey=FiberGIS_CatalogoWeb -Dsonar.sources=src -Dsonar.exclusions=**/node_modules/**"
                            }
                        }
                    }
                }
            }
        }       
        stage('Transfer files to remote server') {
            steps {
                sshagent(['SSH_Server_135_geouser']) {
                    //sh 'ssh user@192.168.1.135 mkdir -p /urs/src/app/fibergis_fgapi/fibergis_catalogoweb'
                    sh 'scp C:/Code/FiberGIS_CatalogoWeb/Dockerfile geouser@192.168.1.135:/usr/src/app/fibergis_catalogoweb/'
                    sh 'scp C:/Code/FiberGIS_CatalogoWeb/nginx.conf geouser@192.168.1.135:/usr/src/app/fibergis_catalogoweb/'
                    sh 'scp -r C:/Code/FiberGIS_CatalogoWeb/CatalogoWeb/dist geouser@192.168.1.135:/usr/src/app/fibergis_catalogoweb/'
                }
            }
        }        
        stage('Build Docker image') {
            steps {
                sshagent(['SSH_Server_135_geouser']) {
                    sh '''
                        ssh geouser@192.168.1.135 "
                            cd /usr/src/app/fibergis_catalogoweb && 
                            if docker ps -a | grep fgcatalogofront >/dev/null 2>&1; then docker stop fgcatalogofront && 
                            docker rm fgcatalogofront; fi && 
                            docker image rm -f fgcatalogofront:qa || true && 
                            docker build -t fgcatalogofront:qa --no-cache /usr/src/app/fibergis_catalogoweb
                        "
                    '''             
                }
            }
        }      
        stage('Run Docker container') {
            steps {
                sshagent(['SSH_Server_135_geouser']) {
                    sh '''
                        ssh geouser@192.168.1.135 "
                            docker run -d --restart=always -p 81:81 --name fgcatalogofront fgcatalogofront:qa
                        "
                    '''
                }
            }
        } 
    } 
    post {
        success {
            emailext body: "La subida de FiberGIS_CatalogoWeb se ha completado con exito.\n\n" +
                           "Ultimo mensaje de commit: ${env.LAST_COMMIT_MESSAGE}\n\n" +
                           "Commit Id: ${env.LAST_COMMIT_HASH}.\n\n" +
                           "CatalogoWeb\n" +
                           "http://192.168.1.135:81\n\n" +
                           "Job Name: ${env.JOB_NAME}\n" +
                           "Build: ${env.BUILD_NUMBER}\n" +
                           "Console output: ${env.BUILD_URL}",  
                     subject: 'FiberGIS_CatalogoWeb - Subida Exitosa',
                     to: 'Raul.Anchorena@geosystems.com.ar;Agustin.David@geosystems.com.ar'
        }
        failure {
            emailext body: "La subida de FiberGIS_CatalogoWeb ha fallado.\n\n" +
                           "Job Name: ${env.JOB_NAME}\n" +
                           "Build: ${env.BUILD_NUMBER}\n" +
                           "Console output: ${env.BUILD_URL}", 
                     subject: 'FiberGIS_CatalogoWeb - La subida ha Fallado - ERROR',
                     to: 'Raul.Anchorena@geosystems.com.ar;Agustin.David@geosystems.com.ar'
        }
    }
}

