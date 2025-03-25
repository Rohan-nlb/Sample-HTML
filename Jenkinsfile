pipeline {
    agent any
    environment {
        GITHUB_REPO = 'https://github.com/Rohan-nlb/Sample-HTML.git'
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
                withCredentials([usernamePassword(credentialsId: 'af20773d-a504-4289-849f-d4ee014836c4', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    script {
                        bat """
                            git config --global user.email "rohan.saini@nlbtech.com"
                            git config --global user.name "rohan-nlb"

                            REM Ensure we are on the correct branch
                            git checkout main
                            git pull origin main

                            REM Create gh-pages branch if it doesn’t exist
                            git branch -r | findstr /C:"origin/gh-pages" >nul || git checkout -b gh-pages
                            git checkout gh-pages
                            git pull origin gh-pages || echo "No remote gh-pages branch yet"

                            REM Deploy the new changes
                            git add .
                            git commit -m "Automated deployment by Jenkins" || echo "No changes to commit"
                            git push "https://%GIT_USERNAME%:%GIT_PASSWORD%@github.com/Rohan-nlb/Sample-HTML.git" gh-pages --force
                        """
                    }
                }
            }
        }
    }
}
