pipeline {
    
    agent any
    
    tools {
        gradle "gradle54"
    }
    
    environment {
        SAAGIE_CREDS = credentials('SaagieCreds')
        SAAGIE_URL = 'https://saagie-manager.prod.saagie.io/api/v1'
    }
    
    stages {

        stage('Cloning repo') {
            steps {
                git branch: 'dataops-plugin', url: 'https://github.com/adrienblind/saagie-cicd.git'
            }
        }
    
        stage ('Deploy on Saagie DEV') {
            environment {
                SAAGIE_PLATFORM = '4'
            }
            steps {
                sh "gradle projectsCreateJob -Psaagieusername=$SAAGIE_CREDS_USR -Psaagiepwd=$SAAGIE_CREDS_PSW -Psaagieplatform=$SAAGIE_PLATFORM -Psaagieurl=$SAAGIE_URL"
            }
        }
        
        stage ('Deploy on Saagie PREPROD') {
            environment {
                SAAGIE_PLATFORM = '4'
            }
            steps {
                input "Deploy to PREPROD ?"
                sh "gradle updateJob -Psaagieusername=$SAAGIE_CREDS_USR -Psaagiepwd=$SAAGIE_CREDS_PSW -Psaagieplatform=$SAAGIE_PLATFORM -Psaagieurl=$SAAGIE_URL"
            }
        }
            
        stage ('Deploy on Saagie PROD') {
            environment {
                SAAGIE_PLATFORM = '4'
            }
            steps {
                input "Deploy to PROD ?"
                sh "gradle updateJob -Psaagieusername=$SAAGIE_CREDS_USR -Psaagiepwd=$SAAGIE_CREDS_PSW -Psaagieplatform=$SAAGIE_PLATFORM -Psaagieurl=$SAAGIE_URL"
            }
        }
    }
}
