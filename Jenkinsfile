#!groovy

node('WindowsVM') {
    
  withEnv(['CI = \'true\'']) {
    dir('PipelineProject') {
        stage('Build') {

           def solutionPath = "\"${tool 'Community'}MSBuild.exe\" PipelineProject.sln"

           echo 'Clean'
           bat "${solutionPath} /t:Clean"
           
           echo 'Restore packages'
           bat "${solutionPath} /t:Restore"
       
           echo 'Building'
           bat "${solutionPath} /p:Configuration=Release /p:Platform=\"x64\""
        }

        stage('Test') {
          echo 'Running tests'
        }
        
        stage('Production') {
          echo 'Deploy to production?'
        }
    }
  }
}

def RunMSBuild(configuration, platform, command=null) {
        def param = command ? '' : "/t:${command}"
        bat "${tool 'Community'}MSBuild.exe PipelineProject\\PipelineProject.sln ${param} /p:Configuration=${configuration} /p:Platform=\"${platform}\""
}
