pipeline {
    agent any
    environment {
        PATH = "/opt/sonar-scanner/bin:$PATH"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'http://172.17.0.1/niko/it_lab_4.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pipx install pytest'
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'sonar-scanner -Dsonar.projectKey=lab_4 -Dsonar.sources=. -Dsonar.host.url=http://sonarqube:9000 -Dsonar.token=sqp_b35a1b5067dd2fa9164488c4370dd1538d4086d0'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pytest --junitxml=report.xml'
            }
        }
    }
    post {
        always {
            junit 'report.xml'
        }
    }
}
