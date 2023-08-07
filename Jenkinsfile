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
                sh 'mvn test'
            }
        }
        stage('tomcat analysis ') {
            steps {
                sh 'mvn test'
            }
        }
    }
}

 
