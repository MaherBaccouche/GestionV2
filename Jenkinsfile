node{
    
    stage("Git Clone"){
        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/MaherBaccouche/GestionV2.git'
    }
    stage("Maven Clean Build"){
        def mavenHome = tool name: "mavenLocal", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
       
    }
    stage("Build Docker Image"){
        sh 'echo hello' 
        sh "docker stop myapp"
        sh "docker rm -f myapp"
        sh "docker image rm -f app:v3"
        sh "docker build -t  app:v3 . "
        sh "docker run -d --name myapp -p 8090:8080 app:v3 "
    }
    stage("Docker Push"){
        withCredentials([string(credentialsId: 'DOCKERHUB', variable: 'DOCKERHUB')]) {
    
        sh "docker login -u maherbaccouche -p ${DOCKERHUB}"
            }
        sh "docker push maherbaccouche/projet-hello-world:v0.2"
      
    }
}
