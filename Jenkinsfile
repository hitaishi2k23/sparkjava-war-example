pipeline {
    agent any
    tools {
        maven 'apache-maven-3.0.1' 
    }

    stages {
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('install') {
            steps {
                sh 'mvn install'
            }
        }
        stage('Hello') {
            steps {
                echo 'Hello World'
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


























