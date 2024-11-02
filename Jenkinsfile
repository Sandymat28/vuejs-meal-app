pipeline {
  agent any 
  
  /*options {
  }*/
  
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_ACCOUNT')
    SSH_CREDENTIALS_ID = 'remote_credentials' // ID des credentials SSH dans Jenkins
    SERVER_IP = '192.168.1.124'
    USERNAME = 'larissa'
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

      stage('Verify SSH Connection') {
            steps {
                sshagent(credentials: [SSH_CREDENTIALS_ID]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} 'echo "Connection successful!"'
                    """
                }
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
  
