pipeline {
    
    agent any
    
    tools {
        gradle "gradle54"
    }

    triggers {
        cron('H */8 * * *')
        pollSCM('* * * * *')
    }
    
    environment {
        SAAGIE_CREDS = credentials('SaagieCreds')
        SAAGIE_URL = 'https://saagie-manager.prod.saagie.io/api/v1'
    }
    
    stages {

        stage('Cloning repo') {
            steps {
                git url: 'https://github.com/adrienblind/saagie-cicd-jenkins-gradle.git'
            }
        }
    
        stage ('Deploy on Saagie DEV') {
            environment {
                SAAGIE_PLATFORM = '4'
            }
            steps {
                sh "gradle updateJob -Psaagieusername=$SAAGIE_CREDS_USR -Psaagiepwd=$SAAGIE_CREDS_PSW -Psaagieplatform=$SAAGIE_PLATFORM -Psaagieurl=$SAAGIE_URL"
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
