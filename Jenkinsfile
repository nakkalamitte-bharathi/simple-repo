pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build Demo Value'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Liinux Test Stage') {
      parallel {
        stage('Liinux Test Stage') {
          steps {
            echo 'Run Linux tests'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows Tests Stage') {
          steps {
            echo 'Run Windows tests'
          }
        }

      }
    }

    stage('Deploy Stage') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok to deploy to production?'
      }
    }

    stage('Deploy Production Stage') {
      steps {
        echo 'Deploy to Prod '
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'nakkalamitte.bharathi@gmail.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}