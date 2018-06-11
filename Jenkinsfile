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
			 sh 'docker stop $(docker ps -a | grep app | awk '{print $1}')'
			 sh 'docker rm $(docker ps -a | grep app | awk '{print $1}')'
			 sh 'docker run -id -p 8081:80 app'
			 sh 'nc -vz localhost 8081'
			}
			post {
				always {
				 sh 'docker container stop app'
				}
			}
		}
		stage('Push Registry') {
			steps {
			 sh 'docker tag app otomas2/app:stable'
			 sh 'docker push otomas2/app:stable'
			}
		}
	}
}
	
