pipeline {
    agent any 
    
    parameters {
        choice choices: ['DEV', 'QA', 'UAT'], name: 'ENV'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm			       
            }
        }
        stage('Build') {
            steps {
                sh '/home/devops/installers/apache-maven-3.9.6/bin/mvn install'
            }
        }
        stage('Deployment') {
            steps {
                script {
                    if (env.ENV == 'DEV') {
                        sh 'cp target/Pipeline.war /home/devops/installers/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been COMPLETED on Dev!"
                    } else if (env.ENV == 'QA') {
                        sh 'cp target/Pipelin.war /home/devops/installers/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been done on QA!"
                    }
                }
            }
        }
    }
    post {
        success {
            script {
                slackSend(channel: "devops2-slack", message: "Pipeline successfully built and deployed to ${env.ENV} environment.")
            }
        }
        failure {
            script {
                slackSend(channel: "devops2-slack", message: "Pipeline build failed in ${env.ENV} environment.")
            }
        }
    }
}
