pipeline {
    environment {
        registryUrl = 'https://registry.hub.docker.com'
        dockerImage = ''
        imageName = 'melioratech/static-web'
        imageTag = 'latest'
    }
    agent any

    stages {
        stage ('Tagging Stable') {
            when {
                branch 'master'
            }
            steps {
                imageTag = 'stable'
            }
        }

        stage('Build Image for Develop') {

            steps {
                script {
                    // docker.build  imageName + ":" + imageTag
                    dockerImage = docker.build  imageName + ":" + imageTag
                }
            }
        }

        stage('Push Image to Registry') {
            steps {
                script {
                    docker.withRegistry('', 'docker-hub') {
                        dockerImage.push()
                    }
                }                            
            }
        }
    }
}