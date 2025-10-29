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
                echo 'Listing files in workspace...'
                bat 'dir'
                echo 'Building Docker image...'
                bat 'docker build -t python-jenkins-task .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                bat 'docker run -d -p 5000:5000 --name python-jenkins-task-container python-jenkins-task'
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
            bat 'docker stop python-jenkins-task-container || exit 0'
            bat 'docker rm python-jenkins-task-container || exit 0'
            cleanWs()
        }
    }
}
