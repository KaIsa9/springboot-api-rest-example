

pipeline {
   agent {
       docker { image 'node:16-alpine' }
   } 
  stages {
    stage('Build'){
      steps{
      sh '#!/bin/sh \n\
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