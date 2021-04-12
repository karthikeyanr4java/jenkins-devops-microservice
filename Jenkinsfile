/**
//Scripted Pipeline
node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
	stage('Integration Test') {
		echo "Integration Test"
	}
}
**/

// Declarative Pipeline
pipeline {
	agent any
	//agent { docker { image 'maven' } }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				//echo 'PATH - $PATH'
				echo 'BUILD Number - $env.BUILD_NUMBER'
				echo 'BUILD ID - $env.BUILD_ID'
				echo 'JOB Name - $env.JOB_NAME'
				echo 'BUILD Tag - $env.BUILD_TAG'
				echo 'BUILD URL - $env.BUILD_URL'
			}
		}
		stage ('Compile') {
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
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				//"docker build -t karthikeyanr4java/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("karthikeyanr4java/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				//"docker build -t karthikeyanr4java/currency-exchange-devops:$env.BUILD_TAG"
				script {
					docker.withRegistry('', 'dockerhubcred') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}
	} 
	post {
		always {
			echo 'I run always'
		}
		success {
			echo 'I run on success'
		}
		failure {
			echo 'I run on Failure'
		}
		changed {
			echo 'When build state is changed. From FAILED to SUCCESS / SUCCESS to FAILED'
		}
	}
}