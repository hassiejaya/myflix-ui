pipeline{
    node {   
    stage('Clone repository') {
        git credentialsId: 'git', url: 'https://github.com/hassiejaya/myflix-ui.git'
    }
    
    stage('Build image') {
       dockerImage = docker.build("assignmentlk/myflix:latest")
    }
    
 stage('Push image') {
        withDockerRegistry([ credentialsId: "assignmentlk-dockerhub", url: "https://hub.docker.com/repository/docker/assignmentlk/myflix" ]) {
        dockerImage.push()
        }
    }    
}
   
}
