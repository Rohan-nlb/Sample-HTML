pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/gitHUb-html-repo.git'
            }
        }
        
        stage('Deploy to Web Server') {
            steps {
                sh '''
                    sudo cp -r sample-html/* /var/www/html/
                    sudo systemctl restart apache2
                '''
            }
        }
    }
}
