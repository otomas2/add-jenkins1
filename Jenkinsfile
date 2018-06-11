pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
			 sh 'docker build -t app .'
			}
		}
		stage('Test') {
			steps {
			 echo 'TEST'
			 sh 'docker run -id -p 8081:80 --name app app:latest'
			 sh 'nc -vz localhost 8081'
			}
			post {
				always {
				 sh 'docker stop app'
				}
			}
		}
		stage('Push Registry') {
			steps {
				withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'user')]) {
			 	 sh 'docker tag app:latest otomas2/app:stable'
			 	 sh 'docker push otomas2/app:stable'
				}
			}
		}
	}
}
	
