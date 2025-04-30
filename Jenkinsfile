pipeline {
    agent any

    stages {
         stage('clean') {
           steps {
               cleanWs()
            }
        }
        stage('git clone') {
            steps {
                git url: "https://github.com/Shaheen8954/2048-game.git", branch: "main"
            }
        }
      
        stage('docker build') {
            steps {
                sh "docker build -t 2048-game ."
            }
        }
        stage('push image on dockerhub') {
            steps {
                withCredentials([usernamePassword(
                    'credentialsId':"dockerhub-cred",
                    passwordVariable:"dockerHubPass",
                    usernameVariable:"dockerHubUser",)]){
                sh 'echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin'
                sh "docker image tag 2048-game ${env.dockerHubUser}/2048-game"
                sh "docker push ${env.dockerHubUser}/2048-game"

                }
            }
        }
        stage('docker run') {
            steps {
                sh "docker run -d -p 8000:8000 --name 2048-game 2048-game"
            }
        }
    }
}
