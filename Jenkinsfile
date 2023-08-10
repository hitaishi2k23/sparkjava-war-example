pipeline {
    agent any
    tools {
        maven 'maven'
    }
    
    stages {
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Install') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('sonarqube analysis') {
            steps {
                sh "mvn sonar:sonar \
        -Dsonar.host.url=http://18.212.25.177:9000 \
        -Dsonar.login=sqa_5f1a68a84a7c8d6f6e32111bd6d56a439ab64d03"
            }
        }
        stage('jfrog ') {
            steps {
                sh 'jf rt u --url=http://3.83.159.63:8082/artifactory --user=admin --password=Admin123  target/*.war  example-repo-local/${BUILD_NUMBER}/sparkjava-hello-world-1.0.war '


            }
        }
       stage("deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'deployed', path: '', url: 'http://34.238.176.115:8080/')], contextPath: 'demoapp', war: 'target/*.war'
            }
           
        }
    }
}

 
