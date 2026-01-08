pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Build & Test') {
            steps {
                dir('.') {
                    sh 'ls -la'
                    sh 'mvn clean test'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
