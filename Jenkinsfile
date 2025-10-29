pipeline {
    agent any

    triggers {
        
        githubPush()
        
        cron('H 10 * * *')
    }

    stages {
        stage('Clone from GitHub') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    dockerImage = docker.build("python-jenkins-task")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                script {
                    dockerImage.run('-p 5000:5000')
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
    }
}
