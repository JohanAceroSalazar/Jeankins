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

            mail(
                to: 'johanacero2509@gmail.com',
                subject: 'Jenkins - Pipeline exitoso',
                body: 'El pipeline se ejecutó correctamente'
            )

            sh '''
            curl -s -X POST "https://api.telegram.org/bot8789165695:AAH5pSsZIS6j451hkOLrx4vjXq9h_vWlFS8/sendMessage" -d "chat_id=5692406827" -d "text=✅ Pipeline exitoso"
            '''
        }

        failure {
            discordSend(
                webhookURL: 'https://discord.com/api/webhooks/1507885135062630403/--KajvUK9qzMtH0qIlMUV6N8Y3dsOavPI9JQaIgjQbt-0DD6U6K2imrNVbzcuV_y-tn6',
                title: 'Jenkins',
                description: '❌ Pipeline falló',
                result: 'FAILURE'
            )

            mail(
                to: 'johanacero2509@gmail.com',
                subject: 'Jenkins - Pipeline falló',
                body: 'El pipeline falló'
            )

            sh '''
            curl -s -X POST "https://api.telegram.org/bot8789165695:AAH5pSsZIS6j451hkOLrx4vjXq9h_vWlFS8/sendMessage" -d "chat_id=5692406827" -d "text=❌ Pipeline falló"
            '''
        }
    }
}