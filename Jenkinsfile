pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS = credentials('af20773d-a504-4289-849f-d4ee014836c4') // Ensure 'github_token' matches the ID from Jenkins credentials
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
                            credentialsId: 'af20773d-a504-4289-849f-d4ee014836c4' // Use the credential ID stored in Jenkins
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
