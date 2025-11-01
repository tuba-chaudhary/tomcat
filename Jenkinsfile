pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    environment {
        WAR_FILE = "target/hello-tomcat-advanced.war"
        TOMCAT_URL = "http://localhost:7080"
        TOMCAT_USER = "tomcatuser"   // replace with your Tomcat username
        TOMCAT_PASSWORD = "yourpassword"   // replace with your Tomcat password
    }

    stages {
        stage('Clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying WAR file to Tomcat...'
                    bat """
                        curl -u "${TOMCAT_USER}:${TOMCAT_PASSWORD}" ^
                        --upload-file "${WAR_FILE}" ^
                        "${TOMCAT_URL}/manager/text/deploy?path=/hello-tomcat-advanced&update=true"
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
