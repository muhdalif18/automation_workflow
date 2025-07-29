pipeline {
  agent any

  tools {
    nodejs "NodeJS_24"
  }

  environment {
    CYPRESS_CACHE_FOLDER = "${WORKSPACE}/.cache/Cypress"
    ALLURE_RESULTS_DIR = 'allure-results'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/muhdalif18/automation_workflow.git'
      }
    }

    stage('Install dependencies') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Run Cypress Tests') {
      steps {
        sh 'npx cypress run'
      }
    }

    stage('Generate Allure Report') {
      steps {
        sh 'npx allure generate --clean'
      }
    }
  }

  /* post {
    always {
      allure([
        includeProperties: false,
        jdk: '',
        results: [[path: 'allure-results']],
        reportBuildPolicy: 'ALWAYS'
      ])
    }
  } */
  post {
  always {
    allure([
      includeProperties: false,
      jdk: '',
      results: [[path: 'allure-results']],
      reportBuildPolicy: 'ALWAYS'
    ])
  }
}

}
