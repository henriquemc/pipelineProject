#!groovy

node('WindowsVM') {
    
  withEnv(['CI = \'true\'']) {
    dir('PipelineProject') {
        stage('Build') {
            steps {

                   def solutionPath = "\"${tool 'Community'}MSBuild.exe\" PipelineProject.sln"

                   echo 'Clean'
                   bat "${solutionPath} /t:Clean"
                   
                   echo 'Restore packages'
                   bat "${solutionPath} /t:Restore"
               
                   echo 'Building'
                   bat "${solutionPath} /p:Configuration=Release /p:Platform=\"x64\""
            }
        }

        stage('Test') {
            steps {
               
               echo 'Running tests'
            }
        }
    }
  }
}

def RunMSBuild(configuration, platform, command=null) {
        def param = command ? '' : "/t:${command}"
        bat "${tool 'Community'}MSBuild.exe PipelineProject\\PipelineProject.sln ${param} /p:Configuration=${configuration} /p:Platform=\"${platform}\""
}



pipeline {
    agent { label 'WindowsVM' }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
           steps {
               dir('PipelineProject')

               def solutionPath = "\"${tool 'Community'}MSBuild.exe\" PipelineProject.sln"

               echo 'Clean'
               bat "${solutionPath} /t:Clean"
               
               echo 'Restore packages'
               bat "${solutionPath} /t:Restore"
               
               echo 'Building'
               bat "${solutionPath} /p:Configuration=Release /p:Platform=\"x64\""

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
