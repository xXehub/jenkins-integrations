pipeline {
    agent any

    environment {
        APP_NAME = 'php-app'
        IMAGE_NAME = "${APP_NAME}:${BUILD_NUMBER}"
        CONTAINER_NAME = "${APP_NAME}-container"
        GITHUB_REPO = 'https://github.com/xXehub/furniture-in.git'
        // Ganti dengan webhook URL Discord Anda
        WEBHOOK_URL = 'https://discord.com/api/webhooks/1319517307277410345/KmUhZyF82LFk6sjZZygvFHSiMfFEv_sowpHv0NtBfKvM8I5hKwI_tx_v9kpbHwPD-UJF'
    }

    stages {
        stage('Notify Start') {
            steps {
                script {
                    discordSend(
                        webhookURL: env.WEBHOOK_URL,
                        content: "🚀 Started Pipeline Build #${BUILD_NUMBER}",
                        embeds: [[
                            title: "${env.JOB_NAME}",
                            description: "Pipeline started",
                            url: env.BUILD_URL,
                            color: 3066993 // Green color for 'Started'
                        ]]
                    )
                }
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: "${GITHUB_REPO}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."

                    discordSend(
                        webhookURL: env.WEBHOOK_URL,
                        content: "📦 Docker image built: ${IMAGE_NAME}",
                        embeds: [[
                            title: "Docker Build",
                            description: "Docker image has been successfully built",
                            color: 3066993 // Green color for success
                        ]]
                    )
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh """
                        docker ps -q --filter name=${CONTAINER_NAME} | xargs -r docker stop
                        docker ps -aq --filter name=${CONTAINER_NAME} | xargs -r docker rm
                        docker run -d --name ${CONTAINER_NAME} -p 8080:80 ${IMAGE_NAME}
                        sleep 10
                    """

                    discordSend(
                        webhookURL: env.WEBHOOK_URL,
                        content: "🐳 Container running at http://localhost:8080",
                        embeds: [[
                            title: "Deployment",
                            description: "Container deployed and running",
                            color: 3066993 // Green color for success
                        ]]
                    )
                }
            }
        }
    }

    post {
        success {
            script {
                discordSend(
                    webhookURL: env.WEBHOOK_URL,
                    content: "✅ Pipeline succeeded!\nImage: ${IMAGE_NAME}\nContainer: ${CONTAINER_NAME}",
                    embeds: [[
                        title: "Build #${BUILD_NUMBER} Successful",
                        description: "Pipeline completed successfully.",
                        color: 3066993 // Green color for success
                    ]]
                )
            }
        }
        failure {
            script {
                discordSend(
                    webhookURL: env.WEBHOOK_URL,
                    content: "❌ Pipeline failed! Check logs for details",
                    embeds: [[
                        title: "Build #${BUILD_NUMBER} Failed",
                        description: "Something went wrong, please check the logs.",
                        color: 15158332 // Red color for failure
                    ]]
                )
            }
        }
    }
}
