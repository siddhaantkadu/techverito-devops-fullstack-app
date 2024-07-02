pipeline {
    agent { 
        label 'MAVEN' 
    }
    options { 
        timeout(time: 1, unit: 'HOURS')
        timestamps()
    }
    environment { 
        GIT_REPO = 'https://github.com/siddhaantkadu/techverito-devops-fullstack-app.git'
        GIT_BRANCH = 'feature/siddhaant'
        DOCKER_IMAGE_NAME = 'siddhaant/techverito-devops-fullstack-app'
        DOCKER_FILE_FRONTEND = 'docker-froentend'
        DOCKER_FILE_BACKEND = 'docker-backend'
    }
    stages {
        stage('Clean Workspace') {
            steps{
                cleanWs()
            }
        }
        stage('Checkout SCM') {
            steps {
                git url: "${env.GIT_REPO}",
                    branch: "${env.GIT_BRANCH}"
            }
        }
        stage('Build Docker Image') {
            parallel { 
                stage('Build Frontend') {
                    steps {
                        sh "docker build -t ${env.DOCKER_IMAGE_NAME}:frontend -f docker/docker-frontend ."
                    }
                }
                // stage('Build Backend') {
                //     steps {
                //         sh "docker build -t ${env.DOCKER_IMAGE_NAME}:backend -f docker/docker-backend ."
                //     }
                // }
            }
        }
        // stage('Push Docker Images') {
        //     steps {
        //         script {
        //             docker.withRegistry('', 'DOCKERHUB_CREDS') {
        //                 sh """
        //                     docker push ${env.DOCKER_IMAGE_NAME}:frontend
        //                     docker push ${env.DOCKER_IMAGE_NAME}:backend
        //                 """
        //             }
        //         }
        //     }
        // }
    }
}