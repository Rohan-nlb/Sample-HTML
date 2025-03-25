pipeline {
    agent any
    environment {
        GITHUB_REPO = 'https://github.com/Rohan-nlb/Sample-HTML.git' // GitHub Repo URL
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
                withCredentials([string(credentialsId: 'af20773d-a504-4289-849f-d4ee014836c4', variable: 'TOKEN')]) {
                    script {
                        bat """
                            git config --global user.email "rohan.saini@nlbtech.com"
                            git config --global user.name "rohan-nlb"

                            REM Fetch the latest changes
                            git fetch origin gh-pages || echo No gh-pages branch yet

                            REM Switch to gh-pages branch (create if it doesn't exist)
                            git branch | findstr /R /C:"\\bgh-pages\\b" >nul && git checkout gh-pages || git checkout -b gh-pages

                            REM Deploy the new changes
                            git add .
                            git commit -m "Automated deployment by Jenkins"
                            git push https://x-access-token:%TOKEN%@github.com/Rohan-nlb/Sample-HTML.git gh-pages --force
                        """
                    }
                }
            }
        }
    }
}
