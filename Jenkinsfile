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
                    // Cambiar la propiedad baseHref en el archivo angular.json                   
                    //bat 'powershell -Command "(Get-Content -Path angular.json -Raw) -replace \\"baseHref\\": \\"/catalogoweb/\\"", \\"baseHref\\": \\"\\" | Set-Content -Path angular.json"'
                    //bat 'powershell -Command "Import-Module Microsoft.PowerShell.Management; (Get-Content -Path angular.json -Raw) -replace \\"baseHref\\": \\"/catalogoweb/\\"", \\"baseHref\\": \\"\\" | Set-Content -Path angular.json"'
                    //bat 'powershell -Command "(Get-Content -Path angular.json -Raw) -replace \\"baseHref\\": \\"/catalogoweb/\\"", \\"baseHref\\": \\"\\" | Out-File -FilePath angular.json -Encoding utf8"'
                    bat 'powershell -Command "(Get-Content -Path angular.json -Raw) -replace \"baseHref\": \"/catalogoweb/\", \"baseHref\": \"\" | Out-File -FilePath angular.json -Encoding utf8"'
                    //powershell -Command "(Get-Content -Path angular.json -Raw) -replace \"baseHref\": \"/catalogoweb/\"", \"baseHref\": \"\"   | cmd.exe /c \"set /p =\" > angular.json"

                    // Instalar las dependencias de la aplicación utilizando npm
                    bat 'npm install'

                    //bat 'npm run build -- --configuration production'
                    // Realizar el build de la aplicación utilizando el comando npm run build:component
                    bat 'npm run build:component'
                }
            }
        }    
        /*stage('Transfer files to remote server') {
            steps {
                sshagent(['SSH_Server_135_geouser']) {
                    //sh 'ssh user@192.168.1.135 mkdir -p /urs/src/app/fibergis_fgapi/fibergis_catalogoweb'
                    sh 'scp C:/Code/FiberGIS_CatalogoWeb/Dockerfile geouser@192.168.1.135:/usr/src/app/fibergis_catalogoweb/'
                    sh 'scp C:/Code/FiberGIS_CatalogoWeb/nginx.conf geouser@192.168.1.135:/usr/src/app/fibergis_catalogoweb/'
                    sh 'scp -r C:/Code/FiberGIS_CatalogoWeb/CatalogoWeb/dist geouser@192.168.1.135:/usr/src/app/fibergis_catalogoweb/'
                    
                    //sh 'ssh geouser@192.168.1.135 "cd /usr/src/app/fibergis_catalogoweb/catalogoweb && rm -rf .browserslistrc && rm -rf .editorconfig && rm -rf .git && rm -rf .gitignore && ls -la"'
                }
            }
        }        
        stage('Build Docker image') {
            steps {
                sshagent(['SSH_Server_135_geouser']) {
                    sh 'ssh geouser@192.168.1.135 "cd /usr/src/app/fibergis_fgapi && docker build -t fgapi:qa --no-cache /usr/src/app/fibergis_fgapi"'             
                }
            }
        }      
        stage('Run Docker container') {
            steps {
                sshagent(['SSH_Server_135_geouser']) {
                    // sh 'ssh geouser@192.168.1.135 "docker run -p 6062:6062 --name fgapi fgapi:qa"'
                    sh 'ssh geouser@192.168.1.135 "if docker ps -a | grep fgapi >/dev/null 2>&1; then docker stop fgapi && docker rm fgapi; fi && docker run -d -p 6062:6062 --name fgapi fgapi:qa"'
                }
            }
        } 
        */   
    } 
    /*post {
        success {
            emailext body: "El pipeline de FiberGIS_CatalogoWeb se ha completado con exito.\n\nUltimo mensaje de commit: ${env.LAST_COMMIT_MESSAGE}\n\n${env.LAST_COMMIT_HASH}",  
                     subject: 'FiberGIS_CatalogoWeb - Pipeline Exitoso',
                     to: 'Raul.Anchorena@geosystems.com.ar;Agustin.David@geosystems.com.ar'
        }
        failure {
            emailext body: 'El pipeline de FiberGIS_CatalogoWeb ha fallado.', 
                     subject: 'FiberGIS_CatalogoWeb - Pipeline Fallido - ERROR',
                     to: 'Raul.Anchorena@geosystems.com.ar;Agustin.David@geosystems.com.ar'
        }
    }*/
}

