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
        /*stage('Build') {
            steps {
                dir('C:\\Code\\CatalogoWeb\\CatalogoWeb') {
                    bat 'npm install'
                    bat 'npm run build -- --configuration production'
                }
            }
        }
        stage('Deploy to IIS') {
            steps {
                bat 'xcopy /Y /S /I /user:%IIS_USER% /password:%env.IIS_PASSWORD% dist\\* \\\\%IIS_SERVER%\\c$\\inetpub\\wwwroot\\fibergis\\%IIS_SITE_NAME%'
                bat "powershell.exe -ExecutionPolicy Bypass -Command \"$script = 'Set-WebConfigurationProperty -Filter /system.webServer/directoryBrowse -Value $false -PSPath ''IIS:\\Sites\\'+$env:IIS_SITE_NAME'''; Invoke-Expression $script; $script = 'Set-WebConfigurationProperty -Filter /system.webServer/rewrite/rules/rule[@name=''Angular routes''] -Value @{stopProcessing=''False''} -PSPath ''IIS:\\Sites\\'+$env:IIS_SITE_NAME'''; Invoke-Expression $script;\""
                
                //variable de entorno seteada en el sistema
                //--> set XCOPY_PASSWORD=contraseña
                //bat 'xcopy /Y /S /I /user:gsystems\Jenkins /k dist\\* \\\\192.168.1.52\\c$\\inetpub\\wwwroot\\fibergis\\catalogoweb'
            }
        }*/
    }
    /*post {
        success {
            emailext body: 'El pipeline de CatalogoWeb se ha completado con exito.', 
                     subject: 'Pipeline exitoso',
                     to: 'Raul.Anchorena@geosystems.com.ar'
        }
        failure {
            emailext body: 'El pipeline de CatalogoWeb ha fallado.', 
                     subject: 'Pipeline fallido',
                     to: 'Raul.Anchorena@geosystems.com.ar'
        }
    }/*    
}
