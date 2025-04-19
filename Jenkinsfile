pipeline {
    
    agent { label 'one' };
    
    stages{
     stage("Code clone"){
         steps{
             git url: "https://github.com/CodeNikitaX/two-tier-flask-app.git", branch: "master"
         }
     }  
     stage("Code Build"){
         steps{
             sh "docker build -t flask-app:latest ."
         }
     }
     stage("Code Test"){
         steps{
             echo "Code Test"
         }
     }
     stage("Code Push to DockerHub"){
         steps{
             withCredentials([usernamePassword(
                 credentialsId: "dockerHubCreds",
                 passwordVariable: "dockerHubPass",
                 usernameVariable: "dockerHubUser"
                 )]){
                     
             sh "docker login -u  ${env.dockerHubUser} -p ${env.dockerHubPass}"
             sh "docker image tag flask-app:latest ${env.dockerHubUser}/two-tier-flask-app:latest"
             sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
             
             }
         }
     }
     stage("Code Deploy"){
         steps{
             sh "docker compose up -d --build flask-app"
         }
     }
    }
    post{
        success{
            script{
                emailext from: 'leuvaniki11@gmail.com',
                to: 'leuvaniki11@gmail.com',
                body: 'Build success',
                subject: 'Build success'    
            }
        }
    }
}
