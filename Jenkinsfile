pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'chaitug/spring-petclinic'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh './mvnw spring-boot:build-image -DskipTests -Dspring-boot.build-image.imageName=${DOCKER_IMAGE}'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 8081:8081 ${DOCKER_IMAGE}'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
