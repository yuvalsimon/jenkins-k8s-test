pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    jenkins: slave
spec:
  containers:
  - name: jnlp
    image: jenkins/jnlp-slave:4.3-9-alpine
    args: ['\$(JENKINS_SECRET)', '\$(JENKINS_NAME)']
    tty: false
  - name: gradle
    image: gradle:6.6.1-jdk8
    command:
    - sleep
    - 200
    tty: true
"""
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