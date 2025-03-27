pipeline {
    agent any
    environment {
        GITHUB_REPO = 'git@github.com:Rohan-nlb/Sample-HTML.git'
        GIT_SSH_COMMAND = 'ssh -i C:/Users/INT1123/.ssh/id_rsa -o StrictHostKeyChecking=no'
    }
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: GITHUB_REPO,
                            credentialsId: 'af20773d-a504-4289-849f-d4ee014836c4'
                        ]]
                    ])
                }
            }
        }

        stage('Deploy to GitHub Pages') {
            steps {
                script {
                    bat """
                        git config --global user.email "rohan.saini@nlbtech.com"
                        git config --global user.name "rohan-nlb"

                        REM Ensure we are on the correct branch
                        git fetch origin main
                        git checkout main
                        git pull origin main

                        REM Create and switch to gh-pages branch
                        git fetch origin gh-pages
                        git checkout gh-pages || git checkout -b gh-pages
                        git pull origin gh-pages || echo "No remote gh-pages branch yet"

                        REM Deploy the new changes
                        git add .
                        git commit -m "Automated deployment by Jenkins" || echo "No changes to commit"
                        git push git@github.com:Rohan-nlb/Sample-HTML.git gh-pages --force
                    """
                }
            }
        }
    }
}
