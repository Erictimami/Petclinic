pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                echo "checking out our code for gitHub"
                git branch: 'main', url: 'https://github.com/Erictimami/Petclinic.git'
            }
        }
         stage('Test') {
            steps {
                echo "running test on marven build"
                sh "mvn clean test"
            }
        }
        stage('Build') {
            steps {
                echo " running the building step to install by packaging the war file"
                sh "mvn clean install"
            }
        }
         stage('Deploy') {
            steps {
                echo " deploying the Apps through pipeline until the tomcat server"
                sshagent(['tomcat-pipeline']) {
                    sh "scp -o StrictHostKeyChecking=no target/petclinic.war tomcatuser@52.14.232.20:/opt/tomcat/webapps"
                }
            }
        }
    }
}
