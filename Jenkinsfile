pipeline {
	agent any
	environment {
		dockerHome = tool "myDocker"
		mavenHome = tool "myMaven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	// agent {
	// 	docker {
	// 		image 'node:21.7'
	// 		args '--env DOCKER_TLS_CERTDIR='
	// 	}
	// }
	stages {
		stage('Checkout') {
			steps {
				echo 'Build'
				sh 'mvn --version'
				sh 'docker --version'
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
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				echo 'Integration Test'
			}
		}
		stage('Package'){
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				dockerImage = docker build --tls-verify=false -t erikrasniqi/currency-exchange-devops:$env.BUILD_Tag
				// script {
				// 	dockerImage = docker.build("erikrasniqi/currency-exchange-devops:${env.BUILD_Tag}")
				// }
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					echo dockerImage
					docker.withRegistry('','dockerhub'){
						dockerImage.push()
						dockerImage.push('latest')
					}
					
				}
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