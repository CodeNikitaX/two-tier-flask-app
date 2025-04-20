@Library("Shared") _
pipeline {
    
    agent { label 'one' };
    
    stages{
        
     stage("Code clone"){
         steps{
             script{
                 clone("https://github.com/CodeNikitaX/two-tier-flask-app.git", "master")   
             }
         }
     } 
     stage("Trivy File System Scan"){
         steps{
             script{
                 trivy()     
             }
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
             script{
                 docker_push("two-tier-flask-app", "flask-app:latest")
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
                subject: 'Build success for Demo CICD.'    
            }
        }
        failure{
            script{
                emailext from: 'leuvaniki11@gmail.com',
                to: 'leuvaniki11@gmail.com',
                body: 'Build failed',
                subject: 'Build failed for Demo CICD'    
            }
        }
    }
}
