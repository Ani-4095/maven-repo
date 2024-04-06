pipeline {
    agent { label 'my-node'}
    tools { maven 'maven-name'}

    stages {
        stage('checkout source code') {
            steps {
                checkout scm
            }
        }

        stage('build package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('deploy to tomcat') {
            steps {
                sshagent(['tommy']) {
                sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.206.96.48:/opt/tomcat9/webapps"
            }
            }
        }

    }
}
