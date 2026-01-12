pipeline {
    agent any
    
    environment{
        REPO_name = "preran1966/calculator_app_e1"
        Tag = "v1.0"
    }

    stages {
        stage('git-checkout') {
            steps {
               git 'https://github.com/Preran-48/CalculatorApp.git'
            }
        }
        stage('build-img') {
            steps {
               bat 'docker build -t %REPO_name%:%Tag% .'
            }
        }
        stage('connection') {
            steps {
               withCredentials([usernamePassword(credentialsId: 'docker-cred-e1-1', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                   bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
               }
            }
        }
        stage('push_img') {
            steps {
               bat 'docker push %REPO_name%:%Tag%'
            }
        }
    }
}
