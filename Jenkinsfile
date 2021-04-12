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
		stage('Build') {
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