pipeline {
  agent any

  triggers {
    pollSCM('H/2 * * * *')   // Poll every 2 minutes (use with care)
  }

  stages {
    stage('Checkout') {
      steps {
        // Use the SCM info Jenkins already used to fetch this Jenkinsfile
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Build step — add your build commands'
        // e.g., sh 'mvn -B -DskipTests clean package'
      }
    }

    stage('Test') {
      steps {
        echo 'Run tests'
        // e.g., sh 'mvn test'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy (placeholder)'
      }
    }
  }
}
