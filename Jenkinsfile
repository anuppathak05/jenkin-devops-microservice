pipeline {
		agent  any
		stages{
			stage("build"){
				steps{
					echo "Build"
					
				}
			}
			stage("Test"){
				steps{
					echo "Test"
				}
			}
			stage("Integration Test"){
				steps{
					echo "Integration Test"
				}
			}
		}
		post{
			always{
				echo "I am awesome I run alwaya"
				}
			}
		success{
			echo "I run when you are successful"
		}
		failure{
			echo "I run when you fail"
		}
}
