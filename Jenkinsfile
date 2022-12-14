

pipeline {
  agent any
  stages {
    stage('Build'){
      steps{
      echo 'Download dependencies'
        withMaven(maven:"maven-386", publisherStrategy: 'EXPLICIT'){
          sh "cd api \n\
          mvn install -DskipTests\n\
          cd .."
          }
        }
    }
    stage('Test'){
          steps{
              echo 'Test'
              }        
    }
    stage('Deploy'){
        steps{
            echo 'Deploy'
            }
          }        
    }
  }