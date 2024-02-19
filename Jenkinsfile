pipeline{
    
    agent { label "dev-server" }
    
    stages{
        
        stage("code"){
            steps{
                git url: "https://github.com/raqeebAKhan/node-todo-cicd.git", branch: "master"
                echo "code cloned"
            }
            
        }
         stage("build and test"){
            steps{
               sh "docker build -t node-app-test-new ."
               echo 'code build' 
            }
            
        }
        stage("scan image"){
            steps{
               echo 'image scanned' 
            }
            
        }
          stage("push"){
            steps{
               withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
               sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
               sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
               sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
               echo 'image pushed'
                }
 
            }
            
        }

         stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'code deployed' 
            }
            
        }
    }
}
