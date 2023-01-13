
pipeline {

    agent any

      stages{
         
          stage('git checkout'){
           
             steps{
                  git branch: 'main', credentialsId: 'd407d89a-7cfe-47ce-883c-385bc6217308', url: 'https://github.com/bisthan/demo-counter-app.git'
             }
          }
          
      }
}