pipeline {
  agent any 
  /*options {
  }*/

  stages {
    stage ('build') {
      steps {
        echo 'Building application '
        sh 'npm install'
      }
    }

    stage ('test') {
      steps {
        echo 'Testing the application'
        sh 'npm test'
      }
    }

   /* stage ('test') {
      steps {
        echo 'Testing the application'
        sh './jenkins/scripts/test.sh'

      }
    } */
  post {
    always {
        echo 'pipeline finished'
      }
    }
  }
}
