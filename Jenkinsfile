pipeline {
    
    agent any
    
    environment {
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
        }
        
    triggers {
        pollSCM 'H * * * *'
    }
    stages {

           

        stage('Package'){
            steps{
                bat "dotnet package"
     }
  }


        stage('Build'){
            steps{
                bat "dotnet build pipelines-dotnet-core.csproj --configuration Release"
                bat "dotnet clean"
                bat "dotnet compile"
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
