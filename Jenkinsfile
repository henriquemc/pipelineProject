#!groovy

pipeline {
    
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                //sh 'npm install'
                echo 'Running sonar'
            }
        }
        stage('Test') {
            parallel(
              sourceAnalisys: {
                  node {
                      echo 'Running sonar'
                  }    
              }, 
            integrationTests: {
                  echo 'Running integration tests'
                  //runTests()
              }
            )
          
        }
      
      input message: "Do you want publish to production?"
      
      stage('Production') {
        
      }
      
      
    }
}
