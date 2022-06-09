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
	//agent is where we run the build for eg: if we want to run in docker
	// agent {
    //     docker { image 'node:16.13.1-alpine' }
    // }
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build') {
			steps{
				echo "Build"
				sh "mvn --version"
				// sh "docker version"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
			
		}
		stage('Test'){
			steps{
				echo "Test"
			}
		}
		stage('Integration Test'){
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
		//unstable
		//changed
	}
}