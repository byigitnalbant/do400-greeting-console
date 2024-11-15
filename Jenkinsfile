pipeline{
    agent{
        label "nodejs"
    }
    stages{
        stage("Install dependencies"){
            steps{
                sh "npm ci"
            }
        }

        stage("Check Style"){
            steps{
                sh "npm run lint"
            }
        }

        stage("Test"){
            steps{
                sh "npm test"
            }
        }
        stage("Build-Docker-Image"){
            steps{
               script{
                def imageName = "my-app:${env.BUILD_NUMBER}"
                sh """
                    docker build -t ${imageName} .
                    docker push registry/image:v1 
                    docker rmi -f \$(docker images -q) || true
                """
               }
            }
        }
        // Add the Release stage here
    }
}
