pipeline {
    agent {
        label "k8agent"
    }
    
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                     container('build-agent') {
                          checkout scm
                     
                  }
               }
            }
        }
        
        stage('Build') { 
            steps { 
                script{
                    container('build-agent') {
                     app = docker.build("underwater")
                    }
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty-2'
            }
        }
        stage('Deploy') {
            steps {
                script{
                    container('build-agent') {
                        docker.withRegistry('https://532019373627.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:aws-ecr-credentials') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                        }  
                    } 
                }
            }
        }
    }
}
