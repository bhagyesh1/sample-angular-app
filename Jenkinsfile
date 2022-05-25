pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {

                sh 'docker build -t sample-angular:v1  .'
                  sh 'docker tag sample-angular devops1010/sample-angular:v1 '
                sh 'docker tag sample-angular devops1010/sample-angular:$BUILD_NUMBER'

          }
        }

  stage('Publish image to Docker Hub') {

            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push devops1010/sample-angular:v1 '
          sh  'docker push devops1010/sample-angular:$BUILD_NUMBER'
        }

          }
        }

      stage('Run Docker container on Jenkins Agent') {

            steps {
                sh "docker run -d -p 4030:80 devops1010/sample-angular"

            }
        }

    }
}
