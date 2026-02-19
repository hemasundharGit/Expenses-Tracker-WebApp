@Library("shared") _
pipeline {
    agent { label 'sundhar' }

    stages {
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps {
                git url: 'https://github.com/hemasundharGit/Expenses-Tracker-WebApp.git', branch: 'main'
            }
        }

        stage('Cleanup') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Build') {
            steps {
                script{
                build("expensetracker-app","latest","hemasundharamkolla")
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose down && docker compose up -d'
            }
        }

        stage('Push into DockerHub') {
            steps {
                script{
                    push("expensetracker-app","latest","hemasundharamkolla")
                }
            }
        }
    }
}


