pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'shamanettar05/myapp2:v1'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerr-cred',   // ✅ FIXED NAME
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat '''
                    echo %PASS%> pass.txt
                    type pass.txt | docker login -u %USER% --password-stdin
                    del pass.txt
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%'
            }
        }

    }
}
