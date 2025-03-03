pipeline {
    agent {
        docker { 
            image 'node:22.14.0-alpine3.21' 
        }
    }

    environment {
        NODE_VERSION = '22'
        BUILD_DIR = 'dist'
        DEPLOY_DIR = '/srv/cicdtest/jenkins'
        DEPLOY_USER = 'root'
        DEPLOY_HOST = '45.127.6.250'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/KaviV23/jenkins-ci-cd-test'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Project') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    ssh "${DEPLOY_DIR}@${DEPLOY_HOST}"
                    sh "rm -rf ${DEPLOY_DIR}/*"
                    sh "exit"
                    sh "scp ${BUILD_DIR} ${DEPLOY_DIR}@${DEPLOY_HOST}:${DEPLOY_DIR}"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
