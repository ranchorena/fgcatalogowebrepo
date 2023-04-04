pipeline {
    agent any
    environment {
        IIS_SERVER = '192.168.1.52'
        IIS_SITE_NAME = 'web.fibergis'
        IIS_USER = 'gystems\\Jenkins'
        //IIS_PASSWORD = ''
    }    
    stages {
        stage('Checkout') {
            steps {
                dir('C:\\Code\\CatalogoWeb') {
                    withCredentials([string(credentialsId: 'Bitbucket_RAToken', variable: 'ACCESS_TOKEN')]) {
                        checkout([$class: 'GitSCM',
                                  branches: [[name: 'master']],
                                  doGenerateSubmoduleConfigurations: false,
                                  extensions: [[$class: 'GitSCMExtension',
                                                submoduleCfg: [[$class: 'SubmoduleOption',
                                                                disableSubmodules: true,
                                                                parentCredentials: true,
                                                                recursiveSubmodules: true,
                                                                reference: '',
                                                                trackingSubmodules: false]]]],
                                  submoduleCfg: [],
                                  userRemoteConfigs: [[url: 'https://'+ URLEncoder.encode("rancho@gsystems.com.ar", "UTF-8") + ':' + URLEncoder.encode(ACCESS_TOKEN, "UTF-8") +'@bitbucket.org/geosystems_ar/fgcatalogofront.git',
                                                       relativeTargetDir: 'CatalogoWeb']]
                                  ])
                    }
                }
            }
        } 

    }   
}
