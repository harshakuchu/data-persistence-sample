pipeline {
    environment {
        registry = "harshakuchu/app01"
        registryCredential = 'docker-creds'
        dockerImage = ''
    }
    agent any
    stages {
        stage ('Cloning Git') {
            steps {
                git branch: 'main', url: 'https://github.com/harshakuchu/data-persistence-sample.git'
            }
        }
        stage ('Building Image') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        stage ('Push Image') {
            steps {
                script {
                     docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage ('Deploy') {
            steps {
                sh 'sudo docker-compose up'
            }
        }
    }
}
