pipeline {
    agent any
    environment {
        PYTHON_PATH = 'C:\\Users\\Yashu Kun\\AppData\\Local\\Programs\\Python\\Python312;C:\\Users\\Yashu Kun\\AppData\\Local\\Programs\\Python\\Python312\\Scripts'
        PATH = "${PATH};C:\\Windows\\System32"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat '''
                set PATH=%PYTHON_PATH%;%PATH%
                pip install -r requirements.txt
                '''
            }
        }
        stage('SonarAnalysis') {
            environment {
                SONAR_TOKEN = credentials('sonarqube-credentials')
            }
            steps {
                bat '''
                set PATH=%PYTHON_PATH%;%PATH%
                sonar-scanner -Dsonar.projectKey=pipeline2 ^
                -Dsonar.sources=. ^
                -Dsonar.host.url=http://localhost:9000 ^
                -Dsonar.token=sqp_ef3d2517182618965f03a3afb0fd8da6cb506099
                '''
            }
        }
    }
    post {
        success {
            echo "Pipeline executed successfully."
        }
        failure {
            echo "Pipeline failed. Please check the logs."
        }
    }
}
