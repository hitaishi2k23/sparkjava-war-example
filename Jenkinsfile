pipeline {
    agent any
    tools {
        maven 'maven3'
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
        -Dsonar.host.url=http://3.83.1.182:9000 \
        -Dsonar.login=sqa_1a01b25a44a1094602cacfe94f36dc888893840d"
            }
        }
        stage('jfrog ') {
            steps {
                sh 'jfrog rt u ~/.jenkins/workspace/fp-java-maven/target/*.war {jfrog repo}'
            }
        }
       stage("deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'deploy', path: '', url: 'http://3.93.218.23:8080/')], contextPath: 'javaapp', war: 'target/*.war'
            }
           
        }
    }
}

 
