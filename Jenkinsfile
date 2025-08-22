pipeline {
    agent { label 'jenkins-agent' }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    tools {
        maven 'maven'
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
    }
}
