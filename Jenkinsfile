pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'Github-Credentials',
                    url: 'https://github.com/mamitianakely/tp_jenkins_triangle.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install -DskipTests'
            }
        }

        stage('Unit Test Execution') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Build the docker image') {
            steps {
                bat 'docker build --tag christa35/triangle:1.0.0 .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhubpass', variable: 'dockerHubPass')]) {
                    bat "docker login -u christa35 -p %dockerHubPass%"
                }
                bat 'docker push christa35/triangle:1.0.0'
            }
        }

    }
}