#!groovy

pipeline {
    agent { label 'WindowsVM' }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
           steps {
               echo 'Building'
               
               //bat 'nuget restore PipelineProject/HMDOdysseyHome.sln'
           	   bat "\"${tool 'Community'}MSBuild.exe\" PipelineProject\\HMDOdysseyHome.sln /p:Configuration=Release /p:Platform=\"x64\""
               
                //msBuild {
                //    msBuildInstallation('Community')
               //     buildFile('PipelineProject/HMDOdysseyHome.sln')
               //     args('Configuration=Release')
              //      args('Platform=x64')
               //     passBuildVariables()
               //     continueOnBuildFailure()
               //     unstableIfWarnings(false)
               //}
                
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


