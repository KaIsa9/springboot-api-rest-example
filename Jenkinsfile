

pipeline {
  agent any
  stages {
    stage('Build'){
      steps{
      echo 'Download dependencies'
//         withMaven(maven:"maven-386", publisherStrategy: 'EXPLICIT'){
//           sh "#!bin/bash -e\n\
//           mvn install -DskipTests"
//           }
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