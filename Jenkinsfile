@Library('jenkins-shared-libraries') _

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
                clone('https://github.com/Shaheen8954/2048-game.git', 'main')
            }
        }
        stage('docker build') {
            steps {
                dockerBuild('2048-game', 'latest', env.dockerHubUser)
            }
        }
        stage('push image on dockerhub') {
            steps {
                dockerPush('2048-game', 'latest', env.dockerHubUser)
            }
        }
        stage('docker run') {
            steps {
                sh "docker stop 2048-game || true; docker rm 2048-game || true"
                sh "docker run -d -p 8000:8000 ${env.dockerHubUser}/2048-game:latest"
            }
        }
    }
}
