pipeline {
  agent any

  tools {
    nodejs 'nodejs' // Use the name you configured in Jenkins → Global Tool Configuration
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/muhdalif18/automation_workflow.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm ci'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'npx cypress run --env allure=true'
      }
    }

    stage('Generate Allure Report') {
      steps {
        bat 'npx allure generate --clean'
      }
    }
  }

  post {
    always {
      allure([
        commandline: 'Allure_CLI', // Must match Global Tool Config name
        includeProperties: false,
        results: [[path: 'allure-results']],
        reportBuildPolicy: 'ALWAYS'
      ])
    }
  }
}
