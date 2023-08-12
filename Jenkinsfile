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
        scannerHome = tool 'SonarQubeScanner'
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
                    def server = Artifactory.server 'myjfrog'
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
         stage('Transfer File and Run Command on Remote Server') {
            steps {
                script {
                    def remoteCommand = 'pwd & hostname & docker build -t app .'
                    def remoteHost = '44.201.178.197'
                    def remoteUser = 'dockeradmin'

                    // Transfer file to remote server
                    sshPublisher(
                        failOnError: true,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'dockertomcat',
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'Dockerfile',
                                        remoteDirectory: "/home/dockeradmin/"
                                    )
                                ]
                            )
                        ]
                    )

                    // Run command on remote server
                    sshPublisher(
                        configName: 'dockertomcat',
                        transfers: [
                            sshTransfer(
                                execCommand: "${remoteCommand}"
                            )
                        ]
                    )
                }
            }
        }
        
 


        
    //    //  stage('sonarqube analysis') {
    //    //      steps {
    //    //          sh "mvn sonar:sonar \
    //    //  -Dsonar.host.url=http://18.212.25.177:9000 \
    //    //  -Dsonar.login=sqa_5f1a68a84a7c8d6f6e32111bd6d56a439ab64d03"
    //    //      }
    //    //  }
    //    //  stage('jfrog ') {
    //    //      steps {
    //    //          sh 'jf rt u --url=http://3.83.159.63:8082/artifactory --user=admin --password=Admin123  target/*.war  example-repo-local/${BUILD_NUMBER}/sparkjava-hello-world-1.0.war '


    //    //      }
    //    //  }
    //    // stage("deploy on test"){
    //    //      steps{
    //    //          deploy adapters: [tomcat9(credentialsId: 'deployed', path: '', url: 'http://34.238.176.115:8080/')], contextPath: 'demoapp', war: 'target/*.war'
    //    //      }
           
    //    //  }
     }
}


 
