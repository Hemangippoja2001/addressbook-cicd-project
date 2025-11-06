pipeline {
  agent any

  environment {
    // <<< EDIT THESE BEFORE PUSHING >>>
    DEPLOY_USER = 'ubuntu'                  // change to your remote user
    DEPLOY_HOST = '203.0.113.12'            // change to your server IP or hostname
    DEPLOY_PATH = '/opt/tomcat/webapps'     // remote Tomcat webapps directory
    CREDENTIAL_SSH = 'deploy-key'           // credential id to add in Jenkins
  }

  triggers {
    // webhook normally triggers; Poll SCM fallback
    pollSCM('H/2 * * * *')   // polls every 2 minutes (ok for assignment)
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
        echo 'Build step — running Maven package'
        sh 'mvn -B -DskipTests clean package'
        archiveArtifacts artifacts: 'target/*.war', fingerprint: true
      }
    }

    stage('Test') {
      steps {
        echo 'Run tests (if any) - currently skipped'
        // To enable: sh 'mvn test'
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        echo "Deploying WAR to ${env.DEPLOY_USER}@${env.DEPLOY_HOST}:${env.DEPLOY_PATH}"
        // Use sshagent plugin and the SSH credential added in Jenkins
        sshagent (credentials: [env.CREDENTIAL_SSH]) {
          // copy the war (allow first-time host key with StrictHostKeyChecking=no)
          sh "scp -o StrictHostKeyChecking=no target/*.war ${env.DEPLOY_USER}@${env.DEPLOY_HOST}:${env.DEPLOY_PATH}/"
          // restart tomcat service (try common service names)
          sh "ssh -o StrictHostKeyChecking=no ${env.DEPLOY_USER}@${env.DEPLOY_HOST} 'sudo systemctl restart tomcat || sudo systemctl restart tomcat9 || sudo systemctl restart tomcat8 || echo restart-failed'"
        }
      }
    }
  }

  post {
    success {
      echo "Pipeline SUCCESS — deployed to ${env.DEPLOY_HOST}"
    }
    failure {
      echo "Pipeline FAILED — check console output"
    }
  }
}
