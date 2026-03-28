pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                sh 'pip install -r requirements.txt --break-system-packages'
                sh 'python3 -m pytest test_app.py -v'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t amna93/cicd-project:latest .'
            }
        }

        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push amna93/cicd-project:latest'
                }
            }
        }
    }
}
