pipeline {
    agent any

    environment {
        DISCORD_WEBHOOK_URL = 'https://discord.com/api/webhooks/1319517307277410345/KmUhZyF82LFk6sjZZygvFHSiMfFEv_sowpHv0NtBfKvM8I5hKwI_tx_v9kpbHwPD-UJF' 
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
