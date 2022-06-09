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
				sh "docker version"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
			
		}
		stage('Compile'){
			steps{
			
				sh 'mvn clean compile'
			}
		}
		stage('Test'){
			steps{
				sh 'mvn test'
			}
		}
		stage('Integration Test'){
			steps{

			echo "Integration Test"
			sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Package'){
			steps{
				sh 'mvn package -DskipTests'
			}
		}
		stage("build docker image"){
			steps{
				//declerative approach
				// "docker build -t rohitmaddiboina/jenkins-microservice:$env.BUILD_TAG"
				script{
					dockerImage = docker.build("rohitmaddiboina/jenkins-microservice:$env.BUILD_TAG")
				}
			}
		}
		stage('Push Image to Docker'){
			steps{
				script{
					dockerImage.withRegistry('','DockerCredentials')
					dockerImage.push();
					dockerImage.push("latest");
					
				}
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