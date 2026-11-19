pipeline{
    agent any
    
    stages{
        stage("Code clone"){
            steps{
                sh "whoami"
           git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
           echo "code cloning successfull"
            }
        }
        stage("Code Build"){
            steps{
            sh "docker build -t notes-app:latest ."
            echo "building is successfull"
            }
        }
        stage("Push to docker hub"){
            steps{
                withCredentials([usernamePassword('credentialsId:"dockerhubCred",passwordVariable:"dockerHubPass",usernameVariable:dockerHubUser')])
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag notes-app:latest vishalojha166/notes-app:latest"
                sh "docker push vishalojha166/notes-app:latest"
            }
        }
        stage("testing"){
            steps{
                echo "testing is completed"
            }
        }
        stage("Deploy"){
            steps{
                sh "docker run -d -p 8000:8000 notes-app:latest"
                echo "deployment is completed"
            }
        }
        
    }
}