def mvn
def buildInfo
pipeline {
  agent any
    tools {
      maven 'Maven'
      jdk 'JAVA_HOME'
    }

  environment {
    SONAR_HOME = "${tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'}"	  
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
          scannerHome = tool 'sonar'
        }
        withSonarQubeEnv('sonar') {
      	  sh """${scannerHome}/bin/sonar-scanner"""
        }
      } 
    }

    
  
   
  }
}   
