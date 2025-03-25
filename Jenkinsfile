pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS = credentials('af20773d-a504-4289-849f-d4ee014836c4') // GitHub Token ID
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

                        REM Fetch the latest changes
                        git fetch origin gh-pages || echo No gh-pages branch yet

                        REM Switch to gh-pages branch (create if it doesn't exist)
                        git branch | findstr /R /C:"\\bgh-pages\\b" >nul && git checkout gh-pages || git checkout -b gh-pages

                        REM Deploy the new changes
                        git add .
                        git commit -m "Automated deployment by Jenkins"
                        git push https://${GITHUB_CREDENTIALS}@github.com/Rohan-nlb/Sample-HTML.git gh-pages --force
                    """
                }
            }
        }
    }
}
