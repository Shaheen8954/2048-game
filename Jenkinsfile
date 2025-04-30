@Library("shared") _
pipeline {
    agent any

    stages {
         stage('clean') {
           steps {
               cleanWs()
            }
        }
        stage("Hello"){
            steps{
               script{
                   hello()
            }
       
        }
   }
        stage('git clone') {
            steps {
                script{
                 clone("https://github.com/Shaheen8954/2048-game.git", "main")
                }
            }
        }
      
        stage("docker build") {
            steps {
               script{
                docker_build ("2048-game .","shaheen8954")
                }
            }
        }
        stage('push image on dockerhub') {
            steps {
               script{
                   docker_push("2048-game","shaheen8954")
                }
            }
        }
        stage('docker run') {
            steps {
                sh "docker run -d -p 8000:8000 shaheen8954/2048-game"
            }
        }
    }
}
