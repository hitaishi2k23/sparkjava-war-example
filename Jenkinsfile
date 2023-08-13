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
         stage('Sonarqube') {
    environment {
        scannerHome = tool 'sonarqube'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=projectkey"
        }

    }
}
        stage('Upload to Artifactory') {
            steps {
                script {
                    def server = Artifactory.server 'jfrog'
                    def uploadSpec = """{
                        "files": [
                            {
                                "pattern": "target/*.war",
                                "target": "example-repo-local/${BUILD_NUMBER}/"
                            }
                        ]
                    }"""
                    def buildInfo = server.upload(uploadSpec)
                    server.publishBuildInfo(buildInfo)
                }
            }
        }
        stage('SSH transfer') {
 script {
  sshPublisher(
   continueOnError: false, failOnError: true,
   publishers: [
    sshPublisherDesc(
     configName: "host",
     verbose: true,
     transfers: [
      sshTransfer(
       sourceFiles: "Dockerfile",
       execCommand: "ls -l"
      )
     ])
   ])
 }
}

     }
}


 
