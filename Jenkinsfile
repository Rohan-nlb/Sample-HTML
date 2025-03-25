pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS = credentials('github_token') // Ensure 'github_token' matches the ID from Jenkins credentials
    }
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/Rohan-nlb/Sample-HTML.git',
                            credentialsId: 'github_token' // Use the credential ID stored in Jenkins
                        ]]
                    ])
                }
            }
        }
        stage('Deploy to Web Server') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
