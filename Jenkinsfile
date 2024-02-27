pipeline {
    agent any
    environment {
        DOCKERHUB_CRED = credentials('dockerhub-cred')
        GITHUB_TOKEN = credentials('github-credentials')
        DOCKER_USERNAME = 'wasshaik'
        DOCKER_REPO = 'wefox'
        APP_NAME = 'stefanprodan/podapp'
        IMAGE_TAG_1 = '6.5.1'
        IMAGE_TAG_2 = '6.5.3'
        IMAGE_NAME_1 = "${DOCKER_USERNAME}/${DOCKER_REPO}/${APP_NAME}:${IMAGE_TAG_1}"
        IMAGE_NAME_2 = "${DOCKER_USERNAME}/${DOCKER_REPO}/${APP_NAME}:${IMAGE_TAG_2}"
    }
    stages {
        stage('Build and Push Image 6.5.1') {
            steps {
                script {
                    git credentialsId: 'github-credentials', url: 'https://github.com/wasshaikh/wefox.git'
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CRED) {
                        def appImage = docker.build(IMAGE_NAME_1, "-f Dockerfile .")
                        appImage.push()
                    }
                }
            }
        }
        stage('Build and Push Image 6.5.3') {
            steps {
                script {
                     git credentialsId: 'github-credentials', url: 'https://github.com/wasshaikh/wefox.git'
                     docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CRED) {
                        def appImage = docker.build(IMAGE_NAME_2, "-f Dockerfile .")
                        appImage.push()
                    }
                }
            }
        }
    }
}
