node ("Node1") {
    def app
    
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }
    
    stage("Prepare build image") {
           app = docker.build("ololo/task20:${env.BUILD_NUMBER}", "-f Dockerfile .")
    }
    
    stage("Run docker container") {
         app = docker.image('ololo/task20:${env.BUILD_NUMBER}').withRun('-p 80:80') {
           
         }
    }
    
    /* stage('Build image') {
        app = docker.build("ololo91/task20")
    }

    stage('Test image') {


        app.inside {
            sh 'echo "Tests passed"'
        }
    }

     stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }   
     } */
}




