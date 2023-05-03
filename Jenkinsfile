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
                    git url: 'https://x-token-auth:ATCTT3xFfGN06AZe4MFMPf8fN8H4LC0_yZb8vtED9eewtRsKS4x1rsitvD1nlzCTNdPXpkufArUfYZPSspjZyauF4jKGM1EqR4L_AmmH9ObmWAJzSzJR7ocVuak2SqxF7AYawIQGnnjBWjJnduwE1o4uHUerliAJYEBSiDP-tJpLWYu8vLRmWvQ=558B95DF@bitbucket.org/geosystems_ar/fgcatalogofront.git', branch: 'master'
                }
            }
        }
        

    }   
}
