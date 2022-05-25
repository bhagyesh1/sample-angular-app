pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
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
			}
		}

		stage('Push') {

			steps {
				bat 'docker push devops1010/sample-angular:v1'
			}
		}
	}

	post {
		always {
			bat 'docker logout'
		}
	}

}
