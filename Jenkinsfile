pipeline {
    agent { label 'jenkins-agent' }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))  // keep only last 5 builds
    }

    tools {
        maven 'maven'
    }

    environment {
        IMAGE_NAME = "my-hello-world-war"   // change to your app name
        IMAGE_TAG  = "v${BUILD_NUMBER}"     // unique tag for each build
    }

    stages {
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh """
                        mvn sonar:sonar \
                          -Dsonar.projectKey=hello-world-war \
                          -Dsonar.projectName="Hello World WAR" \
                          -Dsonar.projectVersion=1.0
                    """
                }
            }
        }

        stage('Build') {
            steps {
                sh "mvn package"
            }
        }

        stage('Publishing Artifacts to Nexus') {
            steps {
                withCredentials([file(credentialsId: 'setting-xml-file', variable: 'MAVEN_SETTINGS')]) {
                    sh "mvn clean deploy --settings $MAVEN_SETTINGS"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                        docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                    """
                }
            }
        }
    }
}
