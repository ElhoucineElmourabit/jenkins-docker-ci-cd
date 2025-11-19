pipeline {
    agent any

    environment {
        registry = "elhoucineelmourabit/jenkinsci"
        registryCredential = 'dockercred'
        dockerImage = '' 
    }

    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/ElhoucineElmourabit/jenkins-docker-ci-cd'
            }
        }

        stage('Building Image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Test Image') {
            steps {
                script {
                     echo "Tests passed"
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}