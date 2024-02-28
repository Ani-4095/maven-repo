pipeline {
    // add your slave label name
    agent { label 'slave-node1'}
    tools{
        maven 'maven-slave'
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
	      sshagent(['tomcat-server-passwd']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@3.85.162.162:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
