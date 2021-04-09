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
	//agent any
	agent { docker { image 'maven:3.8.1' } }
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				echo 'Build'
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