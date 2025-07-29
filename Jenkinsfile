pipeline {
  agent any

  tools {
    nodejs 'NodeJS 24.4.1' // Use the name you configured in Jenkins → Global Tool Configuration
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/muhdalif18/automation_workflow.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npx cypress run --env allure=true'
      }
    }

    stage('Generate Allure Report') {
      steps {
        sh 'npx allure generate --clean'
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
