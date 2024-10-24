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
        sh 'docker build -t matsandy/projetvue:latest .'
        sh 'docker-compose up -d'
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
          sh 'docker push matsandy/projetvue:latest'
        }
      }

     /* stage ('Run') {
        steps {
          echo 'Running application'
          sh 'docker run -p 3000:3000 -d matsandy/mealsapp:latest'
        }
      }*/
    }
  
  post {
    always {
        echo 'pipeline finished'
        echo 'Loging out'
        sh 'docker logout'
      }
    }
  }
  
