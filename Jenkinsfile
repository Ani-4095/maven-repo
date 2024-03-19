pipeline {
    agent { label 'worker-node-label'}
    tools { maven 'maven-tool'}

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
                sshagent[('tomcat-cred')] {
                sh "scp -o StrictHostKeyCheking=no target/maven-web-application.war ec2-user@54.173.109.207:/opt/tomcat9/webapps"
            }
            }
        }

    }
}
