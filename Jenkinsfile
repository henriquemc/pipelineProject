#!groovy

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
               echo 'Clean'
               RunMSBuild(configuration:'Release', platform:'x64', command:'Clean')
               
               echo 'Restore packages'
               
               RunMSBuild(configuration:'Release', platform:'x64', command:'Restore')
                              
               //bat "\"${tool 'Community'}MSBuild.exe\" PipelineProject\\PipelineProject.sln	/t:Restore /p:Configuration=Release /p:Platform=\"x64\""
               
               echo 'Building'
               RunMSBuild(configuration:'Release', platform:'x64')
                              
           	   //bat "\"${tool 'Community'}MSBuild.exe\" PipelineProject\\PipelineProject.sln /p:Configuration=Release /p:Platform=\"x64\""
               
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
