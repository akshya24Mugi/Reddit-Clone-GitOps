pipeline {
    agent any
    enviornment {
          APP_NAME = "reddit-clone-app"
    }
    stages {
      stage("Clean Workspace") {
        steps {
          cleanWs()
        }
      } 
    
      stage("Checkout from SCM") {
          steps  {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/akshya24Mugi/Reddit-Clone-GitOps.git'
          }  
      
      }

      stage("Update the Deployment tags") {

         steps {
             sh """
                 cat deployment.yaml
                 sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                 cat deployment.yaml
             """    
         }
      }

      stage("Push the changed deployment file to GitHub") {
         steps {
             sh """
                 git config --global user.name "akshya24Mugi"
                 git config --global.user.email "akshay24suthar@gmail.com"
                 git add deployment.yaml
                 git commit -m "Updated Deployment Manifest"
             """
             withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default' )]) {
                 sh "git push https://github.com/akshya24Mugi/Reddit-Clone-GitOps.git main"
         
             }
      
         }
      }

      
    }
}
