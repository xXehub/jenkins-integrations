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
                def embed = [
                    title: "Build Sukses :tada:",
                    description: "Job: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: **BERHASIL**",
                    color: 3066993,
                    thumbnail: [
                        url: "https://media.discordapp.net/attachments/1319516985721229315/1319572293512335411/0d12a119ba7c7899f6bb2224e6b31232.webp?ex=676672f7&is=67652177&hm=1f43f91ef18c018e3de28c7e20197e70bfb391c13198d23861803bdc4833c35c&=&format=webp&width=437&height=437" 
                    ],
                    fields: [
                        [
                            name: "Waktu Mulai",
                            value: "${currentBuild.startTimeInMillis}", 
                            inline: true
                        ],
                        [
                            name: "Durasi",
                            value: "${currentBuild.durationString}",
                            inline: true
                        ]
                    ],
                    footer: [
                        text: "Dikirim pada: ${new Date().format('dd-MM-yyyy HH:mm:ss')}" 
                    ]
                ]
                def message = [
                    embeds: [embed]
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
                def embed = [
                    title: "Build Gagal :x:",
                    description: "Job: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: **GAGAL**",
                    color: 15158332,
                    thumbnail: [
                        url: "https://media.discordapp.net/attachments/1319516985721229315/1319572293512335411/0d12a119ba7c7899f6bb2224e6b31232.webp?ex=676672f7&is=67652177&hm=1f43f91ef18c018e3de28c7e20197e70bfb391c13198d23861803bdc4833c35c&=&format=webp&width=437&height=437"
                    ],
                    fields: [
                        [
                            name: "Waktu Mulai",
                            value: "${currentBuild.startTimeInMillis}", 
                            inline: true
                        ],
                        [
                            name: "Durasi",
                            value: "${currentBuild.durationString}",
                            inline: true
                        ]
                    ],
                    footer: [
                        text: "Dikirim pada: ${new Date().format('dd-MM-yyyy HH:mm:ss')}" // Format tanggal
                    ]
                ]
                def message = [
                    embeds: [embed]
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