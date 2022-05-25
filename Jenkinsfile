pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {

                bat 'docker build -t sample-angular:v1  .'
                  bat 'docker tag sample-angular:v1 devops1010/sample-angular:v1 '
                bat 'docker tag sample-angular:v1 devops1010/sample-angular:$BUILD_NUMBER'

          }
        }

  stage('Publish image to Docker Hub') {

            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          bat  'docker push devops1010/sample-angular:v1 '
          bat  'docker push devops1010/sample-angular:$BUILD_NUMBER'
        }

          }
        }

      stage('Run Docker container on Jenkins Agent') {

            steps {
                bat "docker run -d -p 4030:80 devops1010/sample-angular"

            }
        }

    }
}
