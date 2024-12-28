pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/chevalierendormi/SP_Course_4.git', credentialsId: 'access_for_jenkins'
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" Lab4.sln /p:Configuration=Debug /p:Platform=x64 /m'                    
                    } catch (Exception e){
                        echo "Build error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to build failure.")
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        bat '"C:\\pokatak\\sp_rob\\lab4\\Lab4\\x64\\Debug\\Lab4.exe"'                    
                    } catch (Exception e){
                        echo "Test error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to test execution failure.")
                    }
                }
            }
        }
    }

    post {
        always{
            cleanWs()
        }
        failure {
            echo 'Pipeline failed.'
        }
        success {
            echo 'Build and test succeeded!'
        }
    }
}
