

pipeline {
   agent {
       docker { image 'node:16-alpine' }
   } 
  stages {
    stage('Build'){
      steps{
      sh '#!/bin/bash \n\
      node --version'
          
        }
    }
//     stage('Test'){
//           steps{
//               echo 'Test'
//               }        
//     }
//     stage('Deploy'){
//         steps{
//             echo 'Deploy'
//             }
//           }        
    }
  }