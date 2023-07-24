def mvn
def buildInfo
pipeline {
  agent any
    tools {
      maven 'maven3'
    }

  environment {
    SONAR_HOME = "${tool name: 'sonar3', type: 'hudson.plugins.sonar.SonarRunnerInstallation'}"	  
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
	    script {
          scannerHome = tool 'sonar3'
        }
        withSonarQubeEnv('sonar') {
      	  sh """${scannerHome}/bin/sonar-scanner"""
        }
      } 
    }

    
  
   
  }
}   
