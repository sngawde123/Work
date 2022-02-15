pipeline {
    agent any
    environment {
        PATH = "$PATH:/etc/maven/apache-maven-3.8.4/bin"
    }
    stages {
        stage("list env vars") {
            steps {
                sh "printenv | sort"
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }
        stage("SpnarQube analysis") {
            steps {
                withSonarQubeEnv("sonarqube-8.9.2") {
                    sh "mvn sonar:sonar"
                }        
            }
        }                
    }
    post {
        success {
            script{
                emailext attachLog : true, bcc: '', body: " Hi Sender, "

This is an autogenerated email.

{ Build URL = ${env.BUILD_URL}\n
  Build Number =  ${env.BUILD_NUMBER}\n
  Pipeline Name = ${env.JOB_NAME}\n }
"
Thanks, 
    DevOps Team", cc: '', from: '', replyTo: '', subject: "Build Status = ${env.BUILD_STATUS}\n ${env.JOB_NAME}\n ${env.BUILD_NUMBER}", to: 'snehalgawde724@gmail.com'"
            }
        }
        failure {
            script {
                emailext attachLog : true, bcc: '', body: "

This is an autogenerated email.

Build URL =  ${env.BUILD_URL}\n
Build Number = ${env.BUILD_NUMBER}\n
Pipeline Name = ${env.JOB_NAME}\n

Thanks,
DevOps Team", cc: '', from: '', replyTo: '', subject: "Build Status = ${env.BUILD_STATUS}\n ${env.JOB_NAME}\n ${env.BUILD_NUMBER}", to: 'snehalgawde724@gmail.com'"
            }
        }
        
    }
}
