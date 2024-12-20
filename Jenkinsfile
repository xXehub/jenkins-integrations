pipeline {
    agent any

    environment {
        DISCORD_WEBHOOK_URL = 'https://discord.com/api/webhooks/1319563607305879614/wl_fWOlU06vUI4G7N28IvX6GSctpmwS8o20mjicyBkCjxKjt3FhocBb-63NSfaRFV8_I' 
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Running build...'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }
    }

    post {
        success {
            script {
                discordSend(
                    webhookURL: DISCORD_WEBHOOK_URL,
                    content: "Build Sukses :tada:\nJob: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: SUCCESS"
                )
            }
        }
        failure {
            script {
                discordSend(
                    webhookURL: DISCORD_WEBHOOK_URL,
                    content: "Build Gagal :x:\nJob: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: FAILURE"
                )
            }
        }
    }
}
