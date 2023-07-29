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
    stage('SonarQube_Analysis') {
      steps {
	   sh "mvn sonar:sonar \
  -Dsonar.host.url=http://34.207.127.158:9000 \
  -Dsonar.login=sqa_18e79d9de971bdc2b9a89b84b42ffb0babf38aa3"
        }
      } 
	




	  
    }  
}   
