pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                bat "dotnet clean"

                bat "dotnet compile"
            }
        }

        stage('Test'){
            steps {
                
                bat "dotnet test"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('Package'){
            steps {
                
                bat "dotnet package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }

    }

}
