pipeline {
		agent  any
		environment {
			dockerHome = tool 'myDocker'
			mavenHome = tool 'myMaven'
			PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		}
		stages{
			stage("Checkout"){
				steps{
					sh "mvn --version"
					sh "docker version"
					echo "Build"
					echo "PATH $PATH"
					echo "BUILD_NUMBER -  $env.BUILD_NUMBER"
					echo "BUILD_ID -  $env.BUILD_ID"
					echo "BUILD_TAG -  $env.BUILD_TAG"
					echo "BUILD_URL -  $env.BUILD_URL"
					
				}
			}
			stage("Compile"){
				steps {
					sh "mvn clean"
				}
			}
			stage("Test"){
				steps{
					echo "Test"
					sh "mvn test"
				}
			}

			stage("Integration Test"){
				steps{
					echo "Integration Test"
					sh "mvn failsafe:integration-test failsafe:verify"
				}
			}
			stage("Package"){
				steps{
					echo "Integration Test"
					sh "mvn package -DskipTest"
				}
			}
			stage("Build Docker Image") {
				steps {
					// "docker build -t in28min/currency-exchange-devops:$env.BUILD_TAG"
					script {
						dockerImage = docker.build("in28min/currency-exchange-devops:${env.BUILD_TAG}")
					}
				}
			}
			stage("Push Docker Image") {
				steps {
					script {
						docker.withRegistry('','dockerhub') {
							dockerImage.push()
							dockerImage.push("latest")
						}
					}
				}
			}
		}
		post {
			always{
				echo "I am awesome I run alwaya"
				}
			success {
				echo "I run when you are successful"
			}
			failure {
				echo "I run when you fail"
			}
		}
}
