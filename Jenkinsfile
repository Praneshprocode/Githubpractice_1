
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Praneshprocode/Githubpractice_1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '"C:\\Users\\prane\\AppData\\Local\\Programs\\Python\\Python314\\python.exe" -m venv venv'

                bat 'venv\\Scripts\\python.exe -m pip install -r requirements.txt'

                bat 'venv\\Scripts\\python.exe -m pip install playwright pytest-playwright pytest-html'

                bat 'venv\\Scripts\\python.exe -m playwright install chromium'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'if not exist reports mkdir reports'

                bat 'venv\\Scripts\\python.exe -m pytest --browser chromium --html=reports/report.html --self-contained-html'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }

        failure {
            echo 'Build failed. Check the console output.'
        }

        always {
            archiveArtifacts artifacts: 'reports/report.html',
                             allowEmptyArchive: true
        }
    }
}
