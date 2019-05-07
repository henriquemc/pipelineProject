#!groovy

pipeline {
    agent { label 'WindowsVM' }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
           steps {
               echo 'Clean'
               msbuild("Clean","Release", "x64")
               
               echo 'Restore packages'
               msbuild("Restore","Release", "x64")
               
               bat "\"${tool 'Community'}MSBuild.exe\" PipelineProject\\PipelineProject.sln	/t:Restore /p:Configuration=Release /p:Platform=\"x64\""
               
               echo 'Building'
               msbuild("","Release", "x64")
               
           	   bat "\"${tool 'Community'}MSBuild.exe\" PipelineProject\\PipelineProject.sln	 /p:Configuration=Release /p:Platform=\"x64\""
               
                //msBuild {
                //    msBuildInstallation('Community')
               //     buildFile('PipelineProject\HMDOdysseyHome.sln')
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

def msbuild(command, configuration, platform) {
    def param = command ? '' : '/t:${command}'
    bat "${tool 'Community'}MSBuild.exe PipelineProject\\PipelineProject.sln ${command} /p:Configuration=${configuration} /p:Platform=\"${platform}\""
}


