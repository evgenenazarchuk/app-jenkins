pipeline { 
    agent any
    stages {
        stage('Clone repository') { 
            steps {			
		node('Node1') {
			checkout scm
                }
		node('Node2') {
		        checkout scm
		}
            }
        }
        stage('Prepare build image') { 
            steps {
		node('Node1') {
			app_build = docker.build("ololo91/task20:${env.BUILD_NUMBER}", "-f Dockerfile .")
		}
		node('Node2') {
			app_build = docker.build("ololo91/task20:${env.BUILD_NUMBER}", "-f Dockerfile .")
		}
	     }
	}
        stage('Push image') { 
            steps {
		node('Node1') {
			docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
			}
		}
	 	node('Node2') {
			docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
			}
		}
            }
        }
        stage('Run docker container') {
	     steps {
		 node('Node1') {
			sh '''
			if [ $( docker ps -a -f name=task20 | wc -l ) -eq 2 ]; then
				echo "task20 exist"
			else
				echo "testContainer does not exist"
				docker run -d --name task20 -p 80:80 -p 443:443 ololo91/task20
			fi     
			'''
		 }
		 node('Node2') {
			sh '''
			if [ $( docker ps -a -f name=task20 | wc -l ) -eq 2 ]; then
				echo "task20 exist"
			else
				echo "testContainer does not exist"
				docker run -d --name task20 -p 80:80 -p 443:443 ololo91/task20
			fi     
			'''
		}
            }
	}
    }
}

