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
                    // Tambahkan langkah build yang kamu butuhkan di sini
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    // Tambahkan langkah test yang kamu butuhkan di sini
                }
            }
        }
    }

    post {
        success {
            script {
                // Kirim notifikasi ke Discord jika build sukses
                def message = [
                    content: "Build Sukses :tada:\nJob: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: SUCCESS"
                ]
                httpRequest(
                    url: DISCORD_WEBHOOK_URL,
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(message)
                )
            }
        }
        failure {
            script {
                // Kirim notifikasi ke Discord jika build gagal
                def message = [
                    content: "Build Gagal :x:\nJob: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: FAILURE"
                ]
                httpRequest(
                    url: DISCORD_WEBHOOK_URL,
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(message)
                )
            }
        }
    }
}