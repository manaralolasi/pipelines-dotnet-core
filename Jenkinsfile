pipeline {
    
    agent any
    stages {

           

        stage('Restore packages'){
            steps{
                bat "dotnet restore pipelines-dotnet-core.csproj"
     }
  }

        stage('Clean'){
            steps{
                bat "dotnet clean pipelines-dotnet-core.csproj"
     }
   }

        stage('Build'){
            steps{
                bat "dotnet build pipelines-dotnet-core.csproj --configuration Release"
    }
 }

        stage('Test: Unit Test'){
            steps {
                bat "dotnet test pipelines-dotnet-core.csproj"
     }
  }
       
         stage('Test: Integration Test'){
            steps {
                bat "dotnet test pipelines-dotnet-core.csproj"
      }
   }

        stage('Publish'){
            steps{
                bat "dotnet publish pipelines-dotnet-core.csproj"
     }
}

            post{
                always{
    emailext body: "${currentBuild.currentResult}: Job   ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
    recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
    subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
    }
  }
}
