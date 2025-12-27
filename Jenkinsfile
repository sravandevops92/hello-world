pipeline {
    agent any 
    environment {
    }
    parameters {
        string(environment_name: "", decription: "Please enter environment name")
        choice(credentials_id: [dev-credentials_id, sit_credentials_id, uat_credentials_id, prod_credentials-id], decription: "please select the credentailsid"]

   }
   stages {
       stage ('deploy') {
           steps {
               script {
                   println("################# STARTED ${params.environment_name} ENVIORNMENT DEPLOY #############")
                   /// here block of code to read actual credentials withcredentils
                   //sh "aws update-kubeconfig --name my-cluster --reagin us-east-1"
                    def TAG = sh(script: "date +%Y%m%d-%H%M%S", returnStdout: true).trim()
                    env.IMAGE_TAG = TAG
                    def IMAGE_NAME = "dharimigariarjun/maven-project:${env.IMAGE_TAG}"
                    println("$IMAGE_NAME}")
                    sh "sed -i 's|image: .*|image: ${IMAGE_NAME}|' k8s/2-deployment.yml"
                    sh "cat k8s/2-deployment.yml"
                    println("COMPLTED ${params.environment_name} DEPLOYMENT")
               }
           }
       }
  }
}

                                
        
