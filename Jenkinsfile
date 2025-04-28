pipeline {
    agent any

    stages {
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
        stage('docker run') {
            steps {
                sh "docker run -d -p 8000:8000 --name 2048-game 2048-game"
            }
        }
    }
}
