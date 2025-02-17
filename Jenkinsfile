pipeline {
	// agent any
	agent {
		docker {
			image 'node:21.7'
			args '--env DOCKER_TLS_CERTDIR='
		}
	}
	stages {
		stage('Build') {
			steps {
				echo 'Build'
				sh 'node --version'
			}
			post {
				always {
					echo 'I run at the end of the build stage'
				}
			}
		}
		stage('Test') {
			steps {
				echo 'Test'
			}
		}
		stage('Integration Test') {
			steps {
				echo 'Integration Test'
			}
		}
	}
	post {
		always {
			echo 'I always run'
		}
		success {
			echo 'I run when successful'
		}
		failure {
			echo 'I run when failed'
		}
	}
}