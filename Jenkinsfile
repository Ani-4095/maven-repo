pipeline {
    // add your slave label name
    agent { label 'worker-label-0903'}
    tools{
        maven 'maven-test'
    }
    stages {
        stage ('Checkout_SCM') {

            steps {
          	    
	     checkout scm
            }
        }

        stage ('Maven_Build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('Deploy_Tomcat') {

            steps {
	      sshagent(['tomcat-server-key']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@54.166.105.186:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
