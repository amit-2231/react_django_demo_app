pipeline {
    agent any
        
    stages{
        stage("Code"){
            steps {
                echo "cloning the code"
                git url:"https://github.com/amit-2231/react_django_demo_app.git", branch: "main"
        
            }
        }
        
        stage("Build"){
            steps {
                echo "building the code"
                sh "docker build -t my-node-app ."
            }
        }
        
        stage("Push to Docker Hub"){
            steps {
                echo "pushing into dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag  my-node-app ${env.dockerHubUser}/my-node-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-node-app:latest"
                 
                }
            }
        }
        
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
