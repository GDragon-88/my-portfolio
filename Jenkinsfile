pipeline {
    agent any 

    environment {
        // Đặt biến môi trường để chỉ định Docker image cần xóa
        DOCKER_IMAGE = 'my-app'
        DOCKER_CONTAINER_NAME = 'my-app'
        DOCKER_IMAGE_TAG = 'latest'
        DOCKER_IMAGE_NAME = 'my-app' // Define the missing DOCKER_IMAGE_NAME
    }

    stages {
        stage("Clone") {
            steps {
                git "https://github.com/GDragon-88/my-portfolio.git"
            }
        }

        stage('Stop Docker Container') {
            steps {
                script {
                    // Sử dụng Docker CLI để dừng container
                    sh "sudo docker stop ${DOCKER_CONTAINER_NAME}"
                }
            }
        }

        stage('Clean Up Docker Images') {
            steps {
                script {
                    // Sử dụng Docker CLI để xóa Docker image
                    sh "sudo docker rmi ${DOCKER_IMAGE} -f"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Xây dựng Docker image từ Dockerfile trong thư mục hiện tại
                    sh "sudo docker build -t ${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Chạy container từ Docker image đã xây dựng
                    sh "sudo docker run -itd --rm --name $DOCKER_CONTAINER_NAME -p 80:80 ${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG}"
                }
            }
        }
    }
}
