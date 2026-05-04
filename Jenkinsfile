pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
        REGISTRY = 'docker.io'
        DOCKER_IMAGE = "${REGISTRY}/${env.BUILD_USER}/student-doubt-solving"
        DOCKER_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo '✓ Code checked out successfully'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo '📦 Installing dependencies...'
                    sh 'npm install'
                }
            }
        }

        stage('Lint') {
            steps {
                script {
                    echo '🔍 Running ESLint...'
                    sh 'npm run lint'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo '🧪 Running tests...'
                    sh 'npm run test'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo '🏗️ Building application...'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo '🐳 Building Docker image...'
                    sh '''
                        docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
                        docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            when {
                branch 'main'
            }
            steps {
                script {
                    echo '📤 Pushing Docker image to registry...'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh '''
                            echo "${DOCKER_PASS}" | docker login -u "${DOCKER_USER}" --password-stdin
                            docker push ${DOCKER_IMAGE}:${DOCKER_TAG}
                            docker push ${DOCKER_IMAGE}:latest
                            docker logout
                        '''
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                script {
                    echo '🚀 Deploying application...'
                    sh '''
                        docker-compose down || true
                        docker-compose up -d
                    '''
                }
            }
        }
    }

    post {
        always {
            echo '🧹 Cleaning up workspace...'
            cleanWs()
        }
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for details.'
        }
    }
}
