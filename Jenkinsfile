
pipeline{

    agent any

      stages{
         
          stage('git checkout'){
           
             steps{
                  git branch: 'main', credentialsId: 'd407d89a-7cfe-47ce-883c-385bc6217308', url: 'https://github.com/bisthan/demo-counter-app.git'
             }
          }
          stage('unit test'){
           
             steps{
                  sh 'mvn test'     
             }
          }

          stage('integratio testing'){
           
             steps{
                  sh 'mvn verify -DskipUnitTest'     
             }
          }

          stage('maven build'){
           
             steps{
                  sh 'mvn clean install'     
             }
          }

          stage('sonar_analysis'){
             steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                     sh 'mvn clean package sonar:sonar'     
             }
          }
     }
      }

          stage('quality_gate'){
             steps{
               script{
                  waitForQualityGate abortPipeline: false, credentialsId: 'sonar-config'

               }
             }
          }
}
}
