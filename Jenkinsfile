pipeline {
    agent any
    
    stages {
        stage('code'){
            steps {
                echo "cloning the code"
                git url: "https://github.com/vicky941/django-notes-app.git", branch: "main"
            }
        }
        stage('build'){
            steps {
                echo "build the image"
                sh "docker build -t mynotes-app ."
            }
        }
        stage('push to Docker Hub'){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "VICKY@7287", usernameVariable: "venky7287")]){
                    sh "docker tag mynotes-app venky7287/mynotes-app:latest"
                    sh "docker login -u venky7287 -p VICKY@7287"
                    sh "docker push venky7287/mynotes-app:latest"
                }
            }
        }
        stage('deploy'){
            steps {
                echo "deploying the container"
                sh "docker run -d -p 8000:8000 venky7287/mynotes-app:latest"
            }
        }
    }
}
