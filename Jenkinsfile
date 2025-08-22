pipeline {
    agent {
        label 'jenkins-agent'
    }
    tools {
        maven 'maven'
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
                    def SONAR_SCANNER_HOME = tool 'sonar-scanner'  // sonar-scanner must be configured in Global Tool Configuration
                        sh "${SONAR_SCANNER_HOME}/bin/sonar-scanner --version"
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
