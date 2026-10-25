pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        GITHUB_CREDENTIALS = credentials('github')
    }

    stages {
        stage('Docker Hub Login') {
            steps {
                sh '''
                    printf '%s' "$DOCKERHUB_CREDENTIALS_PSW" |
                    docker login -u "$DOCKERHUB_CREDENTIALS_USR" --password-stdin
                '''
            }
        }

        stage('GitHub Registry Login') {
            steps {
                sh '''
                    printf '%s' "$GITHUB_CREDENTIALS_PSW" |
                    docker login ghcr.io \
                    -u "$GITHUB_CREDENTIALS_USR" \
                    --password-stdin
                '''
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mohamedhmza123/first-project.git'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                sh 'ansible-playbook docker-install.yml'
            }
        }
    }
}
