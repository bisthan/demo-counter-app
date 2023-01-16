
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
                    withSonarQubeEnv(credentialsId: 'sonar-config') {
                     sh 'mvn clean package sonar:sonar'     
             }
          }
     }
      }

          stage('uplaod the file into the nexus'){
            steps{

               script{
                  nexusArtifactUploader artifacts:
                      [
                        [
                           artifactId: 'springboot', 
                           classifier: '', 
                           file: 'target/Uber.jar', 
                           type: 'jar'
                           ]
                     ], 
                        credentialsId: 'nexus_id', 
                        groupId: 'com.example', 
                        nexusUrl: '35.89.136.196:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'maven-releases', 
                        version: '1.0.0'
               }
            }
          }
  }
}
