pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Build & Test') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                mkdir -p /opt/app
                cp target/*.jar /opt/app/
                '''
            }
        }
    
    }
}
