pipeline {
    
    agent any
    stages {

           

        stage('Packages'){
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

        stage('Test'){
            steps {
                bat "dotnet test"
     }
  }
       
        stage('Publish'){
            steps{
                bat "dotnet publish"
     }

            post{
                always{
                    emailext body: "${currentBuild.currentResult}: Job   ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                    subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
    }
  }
}
}
}
