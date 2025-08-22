pipeline {
    agent {
        label 'jenkins-agent'
    }

    tools {
        maven 'maven'   // Maven tool configured in Jenkins Global Tool Configuration
    }

    stages {
        stage('Test') {
            steps {
                script {
                    sh "mvn test"
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('sonar') {  // 'sonar' must match your SonarQube server name in Jenkins
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh "mvn package"
                }
            }
        }
    }
}
