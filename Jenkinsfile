pipeline {
  agent any

  environment {
    // Email Extension uses these if set in Jenkins global config
    EMAIL_RECIPIENT = 'sanjevk5826@example.com'  // Replace with your email
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/sksk12312/jenkins-devsecops.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }

    stage('Notify Developer') {
      steps {
        emailext (
          subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
          body: """Hello,

The Jenkins build for job '${env.JOB_NAME}' has completed with status: ${currentBuild.currentResult}.

Please find the attached log for details.

Regards,
Jenkins CI
""",
          to: "${env.EMAIL_RECIPIENT}",
          attachLog: true
        )
      }
    }
  }
}
