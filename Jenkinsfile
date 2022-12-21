node ("Node1") {
    def app
    
    stage('Clone repository') {
      

        checkout scm
    }
    
    stage("Prepare build image") {
           app = docker.build("ololo/task20:${env.BUILD_NUMBER}", "-f Dockerfile .")
    }
    
    stage("Run docker container") {
         app = docker.image("ololo/task20:${env.BUILD_NUMBER}").withRun('-p 80:80 -p 443:443') {
           
         }
    }

     stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }  
     } 
}




