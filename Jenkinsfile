#!groovy

pipeline {
    
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                //sh 'npm install'
                echo 'Building'
            }
        }
        stage('Test') {
            steps {
            //parallel(
            //  sourceAnalisys: {
                      echo 'Running sonar'
           //   }, 
           //  integrationTests: {
          //        echo 'Running integration tests'
                  //runTests()
          //   }
          //  )
            }
        }
      
      ///input message: "Do you want publish to production?"
      
      stage('Production') {
          steps {
            echo 'Building for production'
          }
      }
      
      
    }
}
