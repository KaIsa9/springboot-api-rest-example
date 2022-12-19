

pipeline {
  agent any
  stages {
    stage('Build'){
      steps{
      sh "#! /bin/bash/ -e\n\
      echo \"Build\" "
          
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