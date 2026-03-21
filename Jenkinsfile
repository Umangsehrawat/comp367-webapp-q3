pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        DOCKERHUB_PWD = credentials('CredentialID_DockerHubPWD')
    }

    stages {

        stage('Check out') {
            steps {
                git branch: 'main', url: 'https://github.com/Umangsehrawat/comp367-webapp-q3'
            }
        }

        stage('Build maven project') {
            steps {
                dir('comp367-webapp') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('Unit test') {
            steps {
                dir('comp367-webapp') {
                    bat 'mvn test'
                }
            }
        }

        stage('Docker login') {
            steps {
                bat 'docker login -u umangsehrawat -p %DOCKERHUB_PWD%'
            }
        }

        stage('Docker build') {
            steps {
                dir('comp367-webapp') {
                    bat 'docker build -t umangsehrawat/comp367-webapp:1.0 .'
                }
            }
        }

        stage('Docker push') {
            steps {
                bat 'docker push umangsehrawat/comp367-webapp:1.0'
            }
        }
    }
}
