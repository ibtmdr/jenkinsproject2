pipeline {
    agent any
    triggers {
        pollSCM('H/2 * * * *') 
    }
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
        stage('slack-notification') {
            steps {
                slackSend(
                 color:  "good",
                 message: "<$JOB_URL|$JOB_NAME> ($currentBuild.currentResult): Build <$RUN_DISPLAY_URL|$BUILD_DISPLAY_NAME> ($currentBuild.durationString) : ",
                 baseUrl: "https://devops-ngp9932.slack.com/services/hooks/jenkins-ci",
                 channel: "général"
                 ) 
            }
        }
        stage('mail-notification') {
            steps {
                emailext
                    replyTo: 'build projet', 
                    subject: "$DEFAULT_SUBJECT", 
                    to: 'ibtissammdarbi@gmail.com', 
                    body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""" ,
              
            }
        }
    }
}
