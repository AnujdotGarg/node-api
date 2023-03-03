pipeline {
    agent any
    stages{
        stage("build"){
            steps{
                sh "docker build -t anujgarg01/node-api:$BUILD_NUMBER ."
            }
        }
        stage("scan"){
            steps{
                //sh "trivy image anujgarg01/node-api:$BUILD_NUMBER"
                sh "echo skipping trivy"
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
        stage ("helm package"){
            steps{
                sh "helm package --version $BUILD_NUMBER ./helmchart"
                sh "echo helm install node-api-$BUILD_NUMBER --set image.tag=$BUILD_NUMBER node-api-$BUILD_NUMBER.tgz"
            }
        }
    
    }
}
