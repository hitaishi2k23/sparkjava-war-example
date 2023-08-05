// def mvn
// def buildInfo
// pipeline {
//   agent any
//     tools {
//       maven 'maven3'
//     }

   
//   stages {
//     stage('Execute_Maven') {
// 	  steps {
// 		  sh 'mvn clean install'		                      
//       }
//     }	
//     stage('SonarQube_Analysis') {
//       steps {
// 	   sh "mvn sonar:sonar \
//   -Dsonar.host.url=http://34.207.127.158:9000 \
//   -Dsonar.login=sqa_18e79d9de971bdc2b9a89b84b42ffb0babf38aa3"
//         }
//       } 
pipeline{
    agent any
    tools {
        maven 'maven3' 
    }

    stages{
        stage("test"){
            steps{
                //mvn test
                sh 'mvn test'
                echo "helloworld"
            }
           
        }
        stage("build"){
            steps{
                sh 'mvn install'
                echo "rintu"
            }
           
        }
        stage("deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'deploy', path: '', url: 'http://3.93.218.23:8080/')], contextPath: 'javaapp', war: 'target/*.war'
            }
           
        }
        stage("deploy on prod"){
            steps{
                echo "========executing A========"
            }
           
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
	




	  
    }  
}   
