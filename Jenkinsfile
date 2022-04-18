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
                    sh 'docker build -t harshakuchu/data-persistence .'
                }
            }
        }
        stage ('Deploy Image') {
            steps {
                script {
                    withDockerRegistry(",registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
