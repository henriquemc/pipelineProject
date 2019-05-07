#!groovy

pipeline {
    agent { label 'WindowsVM' }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
               // msBuild {
               //     msBuildInstallation('Community')
               //     buildFile('PipelineProject/HMDOdysseyHome.sln')
               //     args('Configuration=Release')
               //     args('Platform=x64')
               //     passBuildVariables()
               //     continueOnBuildFailure()
               //     unstableIfWarnings(false)
           // }
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
          when {
                branch 'dev'
          }
          steps {
            echo 'Building for production'
          }
      }
      
      
    }
}


