pipeline {
	agent any
	// agent {
	// 	docker {
	// 		image 'node:21.7'
	// 		args '--env DOCKER_TLS_CERTDIR='
	// 	}
	// }
	stages {
		stage('Build') {
			steps {
				echo 'Build'
				// sh 'node --version'
				echo "Path: $Path"
				echo "Build Number: $env.BUILD_NUMBER"
				echo "Build ID: $env.BUILD_ID"
				echo "Build Tag: $env.BUILD_Tag"
				echo "Build URL: $env.BUILD_URL"
				echo "Job Name: $env.Job_Name"
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