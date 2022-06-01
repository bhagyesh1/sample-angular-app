
pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        registry = "devops1010/sample-angular"
        registryCredential = 'dockerHub'
    }
    
    stages{
       stage('DEV Building image') {
           when {
                branch 'dev'
            }
      steps{
        script {
          properties([pipelineTriggers([pollSCM('*/5 * * * *')])])	
          dockerImage = docker.build registry + ":$env.BRANCH_NAME,$BUILD_NUMBER"
          bat "docker run -d -p 4030:80 devops1010/sample-angular:${'env.BRANCH_NAME'}${'BUILD_NUMBER'}"
        }
      }
    }
       /*stage('Run Docker container on DEV Jenkins Agent') {
      steps {
          bat "docker run -d -p 4030:80 devops1010/sample-angular:${'env.BRANCH_NAME'}${'BUILD_NUMBER'}"
            }
        }*/

        stage('BETA Building image') {
            when {
                branch 'beta'
            }
      steps{
        script {
          properties([pipelineTriggers([pollSCM('*/10 * * * *')])])	
          dockerImage = docker.build registry + ":${'env.BRANCH_NAME'}${'BUILD_NUMBER'}"
          bat "docker run -d -p 4031:80 devops1010/sample-angular:${'env.BRANCH_NAME'}${'BUILD_NUMBER'}"
        }
      }
    }
       /*stage('Run Docker container on BETA Jenkins Agent') {
      steps {
          bat "docker run -d -p 4031:80 devops1010/sample-angular:${'env.BRANCH_NAME'}${'BUILD_NUMBER'}"
            }
        }*/
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
