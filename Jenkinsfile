pipeline {
    agent { label 'jenkins-agent' }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    tools {
        maven 'maven'
    }

    environment {
        IMAGE_NAME = "my-hello-world-war"
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
                    def timestamp = new Date().format("yyyyMMdd-HHmmss", TimeZone.getTimeZone('UTC'))
                    def imageTag = "${BUILD_NUMBER}-${timestamp}"

                    sh """
                        docker build -t ${IMAGE_NAME}:${imageTag} .
                    """
                }
            }
        }
    }
}
