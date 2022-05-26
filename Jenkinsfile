pipeline{
    agent any
    triggers{
        cron('0 16 * * 1-5')
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        registry = "devops1010/sample-angular"
        registryCredential = 'dockerHub'
        dockerHubUser= 'devops1010'
        dockerHubPassword= '6e1e4266-081b-4fa0-a1d7-7b07170fc103'
    }
    
    stages{
       stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
       stage('Deploy Image') {
      steps{
         script {
            withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            bat 'docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}'
            dockerImage.push()
          
          }
        }
      }
    }
  }
}
