pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "clone code from suniljmaldiya/my-notes-app repo"
                git url:"https://github.com/suniljmaldiya/my-notes-app.git",branch:"main"
            }
           
            
        }
        stage("Build"){
            steps{
                echo "building the code"
                sh "docker build . -t my-notes-app"
            }
            
            
        }
        stage("Push to docker hub"){
            steps{
                echo "push image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
           
            
        }
        stage("Deploy"){
            steps{
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
