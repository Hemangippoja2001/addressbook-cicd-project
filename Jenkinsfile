pipeline {
  agent any

  triggers {
    pollSCM('H/2 * * * *')   // Poll every 2 minutes (assignment: Poll SCM)
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/<your-username>/<repo>.git', branch: 'main'
      }
    }

    stage('Build') {
      steps {
        echo 'Building...'
        // e.g., mvn -B -DskipTests package OR npm install && npm run build
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        // e.g., mvn test
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy step (mock) - add real deploy commands here'
      }
    }
  }
}
