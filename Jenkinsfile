pipeline {
    environment {
        registry = "harshakuchu/harsha_kuchu"
        registryCredential = 'docker-creds'
        dockerImage = ''
    }
    agent any
    stages {
        stage ('Cloning Git') {
            steps {
                git 'https://github.com/harshakuchu/data-persistence-sample.git'
            }
        }
        stage ('Building Image') {
            steps {
                script {
                    dockerImage = docker.build registry =":$BUILD_NUMBER"
                }
            }
        }
        stage ('Deploy Image') {
            steps {
                script {
                    withDockerRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
