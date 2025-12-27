pipeline {
    agent any

    parameters {
        string(
            name: 'environment_name',
            defaultValue: '',
            description: 'Please enter environment name'
        )
        string(
            name: 'IMAGE_TAG'
            defaultValue: '',
            description: 'Please enter image tag'
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
                    //def TAG = sh(script: "date +%Y%m%d-%H%M%S", returnStdout: true).trim()

                    def IMAGE_NAME = "dharimigariarjun/maven-project:${params.IMAGE_TA}"

                    println("IMAGE NAME: ${IMAGE_NAME}")

                    // Update Kubernetes deployment YAML
                    sh """
                        sed -i 's|image: .*|image: ${IMAGE_NAME}|' k8s/2-deployment.yml
                        cat k8s/2-deployment.yml
                    """
                     withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: "${params.CREDENTIALS_ID}", acccessKeyVariable:  'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                        println("credentials id is: ${params.CREDENTIALS_ID}")
                        println("environemnt name is: ${params.environment_name}")
                        println("Image tag is: ${params.IMAGE_TAG}")
                       //sh "aws eks update-kubeconfig --name staging-demo --region us-east-2" 
                       //sh "kubectl apply -f k8s"
                     }

                    println("################# COMPLETED ${params.environment_name} DEPLOYMENT #################")
                }
            }
        }
    }
}
