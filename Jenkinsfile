pipeline {
    agent none

    stages {
        stage('1'){
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0' }
            }
            environment {
                DOTNET_CLI_HOME = "/tmp/dotnet_cli_home"
            }
            steps{
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
        stage('2'){
            agent {
                docker { image 'node:14-alpine'}
            }
            steps{
                dir("DotnetTemplate.Web"){
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm t'
                    sh 'npm run lint'
                }
            }
        }
    }
}
