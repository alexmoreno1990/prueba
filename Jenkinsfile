#!groovy

pipeline {

	agent any	
	environment { 
        groupId = 'devops'
        msgChannel = 'jenkins-notifications'
     }
   
    stages {
        stage('checkout') {
            steps{
                script{
                    echo "checkout scm"
				}
			}
		}		
        
        stage('prepare') {
			steps{
                script{
					sh "git clean -fdx"
				}
			}
			
		}
        stage('compile') {
			steps{
                script{
					echo "nothing to compile for hello.sh..."
				}	
			}
		}
		
        stage('test') {
			steps{
                script{
					sh "bash test_hello.sh"
				}	
			}
		}
		
        stage('package') {
			steps{
                script{
					sh "tar -cvzf hello.tar.gz hello.sh"
				}
			}		
        }
		
        stage('publish') {
			steps{
                script{
					echo "uploading package..."
				}	
			}
		}	
     
        stage('cleanup') {
			steps{
                script{
					echo "doing some cleanup..."
				}
			}
		}
	}	
		
   post {
    success {
      slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }
    failure {
      slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }
   }


}

    