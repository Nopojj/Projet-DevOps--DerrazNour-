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
                mkdir -p deploy
                cp target/*.jar deploy/
                '''
            }
        }
    }

    // ⬇️ ⬇️ ⬇️ ICI : FIN DU PIPELINE
    post {
        success {
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'SLACK_WEBHOOK')]) {
                sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{"text":"✅ Jenkins Pipeline SUCCESS : Build, Tests & Deploy OK"}' \
                $SLACK_WEBHOOK
                """
            }
        }

        failure {
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'SLACK_WEBHOOK')]) {
                sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{"text":"❌ Jenkins Pipeline FAILED"}' \
                $SLACK_WEBHOOK
                """
            }
        }
    }
}
