pipeline {
    agent any
    environment {
        IIS_SERVER = '192.168.1.52'
        IIS_SITE_NAME = 'web.fibergis'
        IIS_USER = 'gystems\\Jenkins'
        //IIS_PASSWORD = ''
        GITLAB_API_TOKEN = credentials('Bitbucket_RAToken')
    }    
    stages {
        stage('Checkout') {
            steps {
                dir('C:\\Code\\CatalogoWeb') {
                    withCredentials([string(credentialsId: 'Bitbucket_RAToken', variable: 'GITLAB_API_TOKEN')]) {
                         checkout([$class: 'GitSCM',
                                    branches: [[name: 'master']],
                                    doGenerateSubmoduleConfigurations: false,
                                     extensions: [[$class: 'CleanCheckout']],
                                      submoduleCfg: [],
                                      userRemoteConfigs: [[url: "https://raulanchorena@bitbucket.org/geosystems_ar/fgcatalogofront.git",
                                                           credentialsId: 'Bitbucket_RAToken',
                                                           relativeTargetDir: 'CatalogoWeb']]
                                    ])
                        }
                }
            }
        }
        

    }   
}
