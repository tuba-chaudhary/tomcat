pipeline {
    agent any

    stages {
        stage('Build WAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying WAR file to Tomcat...'
                bat '''
                curl -u "tomcatuser:yourpassword" ^
                --upload-file "target/hello-tomcat-advanced.war" ^
                "http://localhost:8070/manager/text/deploy?path=/hello-tomcat-advanced&update=true"
                '''
            }
        }
    }
}
