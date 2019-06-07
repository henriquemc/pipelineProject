#!groovy

node('WindowsVM') {
    
  withEnv(['CI = \'true\'']) {
    dir('PipelineProject') {
        stage('Build') {
           echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
           
           def solutionPath = "\"${tool 'Community'}MSBuild.exe\" PipelineProject.sln"

           echo 'Clean'
           bat "${solutionPath} /t:Clean"
           
           echo 'Restore packages'
           bat "${solutionPath} /t:Restore"
       
           echo 'Building'
           bat "${solutionPath} /p:Configuration=Release /p:Platform=\"x64\""

           echo 'Archiving'

        }

        stage 'QA'
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



        stage('Deploy') {
          if (currentBuild.result == null || currentBuild.result == 'SUCCESS') {
              echo 'Publish to store'
          }
        }

    }
  }
}

def RunMSBuild(configuration, platform, command=null) {
        def param = command ? '' : "/t:${command}"
        bat "${tool 'Community'}MSBuild.exe PipelineProject.sln ${param} /p:Configuration=${configuration} /p:Platform=\"${platform}\""
}