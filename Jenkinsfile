pipeline{

	agent any

	environment {
		//DOCKERHUB_CREDENTIALS=credentials('dockerHub')
    DOCKERHUB_CREDENTIALS_PSW='6e1e4266-081b-4fa0-a1d7-7b07170fc103'
    DOCKERHUB_CREDENTIALS_USR='devops1010'
	}

	stages {
	    

		stage('Build') {

			steps {
				bat 'docker build -t devops1010/sample-angular:v1 .'
			}
		}

		stage('Login') {

			steps {
        bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				//bat 'docker login -u devops1010 --password-stdin 6e1e4266-081b-4fa0-a1d7-7b07170fc103'
			}
		}

		stage('Push') {

			steps {
				bat 'docker push devops1010/sample-angular:v1'
			}
		}
          
        stage('Run Docker container on Jenkins Agent') {

            steps {
                bat "docker run -d -p 4030:80 devops1010/sample-angular:v1"
            }
        }
	}

}
