def mvn
def buildInfo
pipeline {
  agent any
    tools {
      maven 'maven3'
    }

   
  stages {
    stage('Execute_Maven') {
	  steps {
		  sh 'mvn clean install'		                      
      }
    }	
    stage('War rename') {
	  steps {
		  	sh 'mv target/*.war target/helloworld.war'
        }			                      
      }
    stage('SonarQube_Analysis') {
      steps {
	   sh "mvn sonar:sonar \
  -Dsonar.host.url=http://18.207.190.98:9000 \
  -Dsonar.login=b44f2ef23b740585326b92c191564bc580ea84e6"
        }
      } 
	




	  
    }  
}   
