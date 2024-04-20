pipeline {
    agent {
        label "firstAgent"
    }

    stages {
        stage('Git checkout') {
            steps {
                echo "checking out our code for gitHub"
                git branch: 'main', url: 'https://github.com/Erictimami/Petclinic.git'
            }
        }
        stage('Validate') {
            steps {
                echo "validating our maven build"
                 sh "mvn clean validate"
            }
        }
         stage('Test') {
            steps {
                echo "running test on marven building"
                sh "mvn clean test"
            }
        }
        stage('Build') {
            steps {
                echo " running the building step to install by packaging the war file"
                sh "mvn clean install"
            }
        }
        stage('Deploy to Stage') {
            steps {
                echo "Deploying our war file into our tomcat Stage server"
                sshagent(['tomcat-pipeline']) {
                     sh "scp -o StrictHostKeyChecking=no target/petclinic.war tomcat@3.21.185.94:/opt/tomcat/webapps"
                }
            }
        }    
        
    }
}
