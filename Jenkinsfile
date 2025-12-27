pipeline {
    agent any

    parameters {
        string(
            name: 'environment_name',
            defaultValue: '',
            description: 'Please enter environment name'
        )

        choice(
            name: 'CREDENTIALS_ID',
            choices: [
                'dev-credentials-id',
                'sit-credentials-id',
                'uat-credentials-id',
                'prod-credentials-id'
            ],
            description: 'Please select the credentials id'
        )
    }

    stages {
        stage('Deploy') {
            steps {
                script {
                    println("################# STARTED ${params.environment_name} ENVIRONMENT DEPLOY #################")

                    // Generate image tag
                    def TAG = sh(
                        script: "date +%Y%m%d-%H%M%S",
                        returnStdout: true
                    ).trim()

                    env.IMAGE_TAG = TAG
                    def IMAGE_NAME = "dharimigariarjun/maven-project:${env.IMAGE_TAG}"

                    println("IMAGE NAME: ${IMAGE_NAME}")

                    // Update Kubernetes deployment YAML
                    sh """
                        sed -i 's|image: .*|image: ${IMAGE_NAME}|' k8s/2-deployment.yml
                        cat k8s/2-deployment.yml
                    """

                    println("################# COMPLETED ${params.environment_name} DEPLOYMENT #################")
                }
            }
        }
    }
}
