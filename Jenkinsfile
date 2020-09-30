pipeline {
    agent {
        kubernetes {
            yamlFile 'jenkins-pod.yaml'
        }
    }
    stages {
        stage('Build') {
            steps {
                container('gradle') {
                    sh 'gradle build -x test'
                }
            }
        }
        stage('Unit tests') {
            steps {
                container('gradle') {
                    sh 'gradle test'
                }
            }
        }
    }
}