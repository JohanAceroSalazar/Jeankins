pipeline {
    agent any

    stages {

        stage('Build and Test') {
            steps {
                sh 'mvn clean verify'
            }
        }

    }

    post {

        always {
            junit testResults: 'target/surefire-reports/*.xml',
                   allowEmptyResults: true
        }

        success {
            discordSend(
                webhookURL: 'https://discord.com/api/webhooks/1507885135062630403/--KajvUK9qzMtH0qIlMUV6N8Y3dsOavPI9JQaIgjQbt-0DD6U6K2imrNVbzcuV_y-tn6',
                title: 'Jenkins',
                description: '✅ Pipeline exitoso',
                result: 'SUCCESS'
            )

            telegramSend(
                message: '✅ Pipeline exitoso'
            )
        }

        failure {
            discordSend(
                webhookURL: 'https://discord.com/api/webhooks/1507885135062630403/--KajvUK9qzMtH0qIlMUV6N8Y3dsOavPI9JQaIgjQbt-0DD6U6K2imrNVbzcuV_y-tn6',
                title: 'Jenkins',
                description: '❌ Pipeline falló',
                result: 'FAILURE'
            )

            telegramSend(
                message: '❌ Pipeline falló'
            )
        }
    }
}