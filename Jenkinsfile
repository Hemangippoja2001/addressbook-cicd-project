pipeline {
    agent any
    triggers {
        pollSCM('H/10 * * * *') // Every minute
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Hemangippoja2001/addressbook-cicd-project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
