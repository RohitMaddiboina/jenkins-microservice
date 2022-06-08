// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// }

//Declerative pipeline
pipeline{
	agent any
	stages{
		stage('Build') {
			steps{
				echo "Build"
			}
			
		}
		stage('Test'){
			steps{

			echo "Test"
			}
		}
		stage('Integr{ation Test'){
			steps{

			echo "Integration Test"
			}
		}
	}
	
	post{
		always {
			echo "I run always"
		}
		success{
			echo "I run build success"
		}
		failure{
			echo "I run build failure"
		}
	}
}