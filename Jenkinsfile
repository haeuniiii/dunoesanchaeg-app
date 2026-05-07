pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
    - name: maven
      image: maven:3.9.9-eclipse-temurin-17
      command:
        - cat
      tty: true
    - name: node
      image: node:20
      command:
        - cat
      tty: true
"""
        }
    }

    stages {
        stage('Backend Build') {
            steps {
                container('maven') {
                    dir('backend') {
                        sh 'mvn clean package -DskipTests'
                    }
                }
            }
        }

        stage('Frontend Build') {
            steps {
                container('node') {
                    dir('frontend') {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
            }
        }
    }
}