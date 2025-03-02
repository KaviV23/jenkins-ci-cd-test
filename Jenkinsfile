pipeline {
    agent any 

    environment {
        NODE_VERSION = '22'
        BUILD_DIR = 'dist'
        DEPLOY_DIR = '/srv/cicdtest/jenkins'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/KaviV23/jenkins-ci-cd-test'
            }
        }
        stage('Setup Node.js') {
            steps {

                script {
                    sh "nvm use ${NODE_VERSION}"
                }
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
                    sh "rm -rf ${DEPLOY_DIR}/*"
                    sh "cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/"
                }
            }
        }
        stage('Publish Artifacts') {
            steps {
                echo 'Save the assemblies generated from the compilation' 
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
