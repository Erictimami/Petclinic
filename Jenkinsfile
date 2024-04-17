pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Erictimami/Petclinic.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }
         stage('Deploy') {
            steps {
                sshagent(['tomcat-pipeline']) {
                    sh "scp -o StrictHostKeyChecking=no target/petclinic.war tomcatuser@52.14.232.20:/opt/tomcat/webapps"
                }
            }
        }
    }
}
