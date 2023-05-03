pipeline {
    agent any
    /*environment {
        //IIS_SERVER = '192.168.1.52'
        //IIS_SITE_NAME = 'web.fibergis'
        //IIS_USER = 'gystems\\Jenkins'
        //IIS_PASSWORD = ''
        //GITLAB_API_TOKEN = credentials('Bitbucker_user_pwd')
    }*/    
    stages {
        stage('Checkout') {
            steps {
                bat 'echo ${env.FG_CATALOGO_BITBUCKET_TOKEN}'
                
                dir('C:\\Code\\CatalogoWeb') {
                    /*withCredentials([string(credentialsId: 'Bitbucker_user_pwd', variable: 'GITLAB_API_TOKEN')]) {
                         checkout([$class: 'GitSCM',
                                    branches: [[name: 'master']],
                                    doGenerateSubmoduleConfigurations: false,
                                     extensions: [[$class: 'CleanCheckout']],
                                      submoduleCfg: [],
                                      userRemoteConfigs: [[url: "https://raulanchorena@bitbucket.org/geosystems_ar/fgcatalogofront.git",
                                                           credentialsId: 'Bitbucket_RAToken',
                                                           relativeTargetDir: 'CatalogoWeb']]
                                    ])
                        }*/
                    git url: 'https://x-token-auth:${env.FG_CATALOGO_BITBUCKET_TOKEN}@bitbucket.org/geosystems_ar/fgcatalogofront.git', branch: 'master'
                }
            }
        }
        /*stage('Build') {
            steps {
                dir('C:\\Code\\CatalogoWeb') {
                    bat 'npm install'
                    bat 'npm run build -- --configuration production'
                }
            }
        } */       

    }   
}
