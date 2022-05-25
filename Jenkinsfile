pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerHub')
  }
  stages {
    stage('Docker Build and Tag') {
      steps {

        bat 'docker build -t devops1010/sample-angular:v1 .'

      }
    }

    stage('Login & Publish image to Docker Hub') {

      steps {
            
        bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        bat 'docker push devops1010/sample-angular:v1 '
        bat 'docker logout'

      }

    }

    stage('Run Docker container on Jenkins Agent') {

      steps {
        
        bat "docker run -d -p 4030:80 devops1010/sample-angular:v1"

      }
   }


  }
  

}
