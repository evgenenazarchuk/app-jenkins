node ("Node1") {
    //def app
    def app_build
    def app_run
    
    environment{
        registry = 'ololo91/task20'
        registryCredential = 'docker-hub-credentials'        
    }
    
    stage('Clone repository') {
        checkout scm
    }
    
    stage("Prepare build image") {
        app_build = docker.build('${env.registry}:latest', '-f Dockerfile .')
    }
    
    stage('Push image') {
        docker.withRegistry('', 'docker-hub-credentials') {
           // app_build.push("${env.BUILD_NUMBER}")
             app_build.push("latest")
        }  
     } 
    
    stage("Run docker container") {
        //app_run = docker.image("ololo91/task20:${env.BUILD_NUMBER}").withRun('-p 80:80 -p 443:443') { 
         //}
       // sh 'docker run -d -p 80:80 -p 443:443 ololo91/task20'
        //sh 'docker rmi -f ololo91/task20'
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




