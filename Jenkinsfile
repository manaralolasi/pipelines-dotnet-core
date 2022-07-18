pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                sh "dotnet clean"

                sh "dotnet compile"
            }
        }

        stage('Test'){
            steps {
                
                sh "dotnet test"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('Package'){
            steps {
                
                sh "dotnet package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }

    }

}
