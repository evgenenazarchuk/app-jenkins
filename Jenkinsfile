node ("Node1") {
    //def app
    def app_build
    def app_run
    
    stage('Clone repository') {
      

        checkout scm
    }
    
    stage("Prepare build image") {
          app_build = docker.build("ololo91/task20:latest", "-f Dockerfile .")
    }
    
    stage('Push image') {
        //docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
           // app_build.push("${env.BUILD_NUMBER}")
            app_build.push("latest")
        //}  
     } 
    
    stage("Run docker container") {
        //app_run = docker.image("ololo91/task20:${env.BUILD_NUMBER}").withRun('-p 80:80 -p 443:443') { 
         //}
       // sh 'docker run -d -p 80:80 -p 443:443 ololo91/task20'
        //sh 'docker rmi -f ololo91/task20'
        sh '''
        docker run -d --name task20 -p 80:80 -p 443:443 ololo91/task20
        '''
    }

     
}




