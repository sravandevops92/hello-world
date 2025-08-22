pipeline {
    agent {
        label 'jenkins-agent'
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))  // keep last 5 builds only
    }

    tools {
        maven 'maven'   // Maven tool configured in Jenkins Global Tool Configuration
    }

    stages {
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {  // 'sonar' must match your SonarQube server name in Jenkins
                    sh "mvn sonar:sonar"
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
    }
}
