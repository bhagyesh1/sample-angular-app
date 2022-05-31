// Multi-branch pipeline. Build once a day from a "dev" branch only
CRON_SETTINGS = BRANCH_NAME == "dev" ? '''20 15 * * *'''
// Multi-branch pipeline. Build once a day from a "beta" branch only
CRON_SETTINGS = BRANCH_NAME == "beta" ? '''40 15 * * *'''
// Multi-branch pipeline. Build once a day from a "master" branch only
CRON_SETTINGS = BRANCH_NAME == "master" ? '''10 16 * * *'''

pipeline{
    agent any
    triggers{
        parameterizedCron(CRON_SETTINGS)
      
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        registry = "devops1010/sample-angular"
        registryCredential = 'dockerHub'
    }
    
    stages{
       stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
       stage('Run Docker container on Jenkins Agent') {
      steps {
          bat "docker run -d -p 4030:80 devops1010/sample-angular:$BUILD_NUMBER"
            }
        }
       /*stage('Deploy Image') {
      steps{
         script {
           docker.withRegistry( '', registryCredential ) {
             dockerImage.push("$BUILD_NUMBER")
              dockerImage.push('latest')
          
          }
        }
      }
    }*/
  }
 }
