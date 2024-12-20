pipeline {
    agent any

    environment {
        DISCORD_WEBHOOK_URL = 'https://discord.com/api/webhooks/1319517307277410345/KmUhZyF82LFk6sjZZygvFHSiMfFEv_sowpHv0NtBfKvM8I5hKwI_tx_v9kpbHwPD-UJF' // Ganti dengan URL webhook yang kamu dapatkan
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
                def message = """
                {
                    "embeds": [
                        {
                            "title": "Build Sukses :tada:",
                            "description": "Job: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: SUCCESS",
                            "color": 3066993
                        }
                    ]
                }
                """
                httpRequest(
                    url: DISCORD_WEBHOOK_URL,
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: message
                )
            }
        }
        failure {
            script {
                def message = """
                {
                    "embeds": [
                        {
                            "title": "Build Gagal :x:",
                            "description": "Job: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: FAILURE",
                            "color": 15158332
                        }
                    ]
                }
                """
                httpRequest(
                    url: DISCORD_WEBHOOK_URL,
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: message
                )
            }
        }
    }
}
