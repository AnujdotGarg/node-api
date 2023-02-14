pipeline {
    agent any
    stages{
        stage("build"){
            steps{
                sh "docker build anujgarg01/node-api:$BUILD_NUMBER ."
            }
        }
        stage("scan"){
            steps{
                sh "trivy image anujgarg01/node-api:$BUILD_NUMBER"
            }
        }
        stage ("push"){
            
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                    sh "docker login docker.io -u $USERNAME -p $PASSWORD"
                    sh "docker push anujgarg01/node-api:$BUILD_NUMBER"
                }
            }
        }
    }
}
