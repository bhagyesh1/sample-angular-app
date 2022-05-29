properties([pipelineTriggers([pollSCM('25 18 * * *')])])	
pipeline{
    agent any
    /*triggers{
        pollSCM ('20 14 * * *')
        //cron "31 11 * * *"
    }*/
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
