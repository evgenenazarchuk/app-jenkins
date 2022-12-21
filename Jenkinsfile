node ("Node1") {
    def app
    def app_build
    def app_run
    
    stage('Clone repository') {
      

        checkout scm
    }
    
    stage("Prepare build image") {
           app = docker.build("ololo/task20:${env.BUILD_NUMBER}", "-f Dockerfile .")
    }
    
    stage("Run docker container") {
         app_run = docker.image("ololo/task20:${env.BUILD_NUMBER}").withRun('-p 80:80 -p 443:443') {
           
         }
    }

     stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app_build.push("${env.BUILD_NUMBER}")
            app_build.push("latest")
        }  
     } 
}




