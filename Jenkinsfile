pipeline {
  agent {
    docker {
      image 'node:alpine'
    }
  }
  stages {
    stage ('install dependencies') {
      steps {
        sh 'yarn install'
      }
    }
    stage ('lint') {
      steps {
        sh 'yarn lint'
      }
    }
    stage ('integration test') {
      steps {
        sh 'yarn test:ci'
      }
      post {
        always {
          junit 'output/test-results/**/*.xml'
          publishHTML target: [
            allowMissing         : false,
            alwaysLinkToLastBuild: false,
            keepAll              : true,
            reportDir            : 'output/test-coverage/lcov-report',
            reportFiles          : 'index.html',
            reportName           : 'Coverage report'
          ]
        }
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
