pipeline{
    agent any
    
    stages{
        stage("clone code"){
            steps{
                echo "cloning the code"
                git url:"https://github.com/amit91088/django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps{
                echo "building an image"
                sh "docker build -t my-note-app ."
            }
            
        }
        stage("push image to DOCKERhub"){
            steps{
                echo "pushing image to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHUB",passwordVariable:"dockerHUBpass",usernameVariable:"dockerHUBuser")]){
                sh "docker tag my-note-app ${env.dockerHUBuser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHUBuser} -p ${env.dockerHUBpass}"
                sh "docker push ${env.dockerHUBuser}/my-note-app:latest"
                }
                
            }
            
        }
        stage("deploy"){
            steps{
                echo "deploying a container"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
