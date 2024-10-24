pipeline {
  agent any 
  
  /*options {
  }*/
  
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_ACCOUNT')
  }
    
  stages {
    stage ('Install dependancies') {
      steps {
        echo 'Installing dependancies'
        sh 'npm install'
      }
    }

    stage ('test') {
      steps {
        echo 'Testing the application'
        sh 'npm test'
        }
    }

    stage ('build') {
      steps {
        echo 'Building docker image'
        sh 'docker build -t matsandy/mealsapp:latest .'
      }
    }

     stage ('login') {
       steps {
        echo 'Loging Dockerhub'
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        }
      }

      stage('Push') {
        steps {
          echo 'Pushing to Dockerhub'
          sh 'docker push matsandy/mealsapp:latest'
        }
      }

      stage ('Run') {
        steps {
          sh 'docker run -d
    }
  
  post {
    always {
        echo 'pipeline finished'
        echo 'Loging out'
        sh 'docker logout'
      }
    }
  }
  
