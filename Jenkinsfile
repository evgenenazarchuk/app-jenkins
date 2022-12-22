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
    }
}


