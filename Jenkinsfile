pipeline {
    agent {
        label 'agent-1'
}
tools {
    maven 'maven'
}
stages {
    /*stage ('checkout'){
        steps {
            script {
                git branch: 'main', url: 'https://github.com/sravandevops92/hello-world.git'
                sh "ls -la"
            }
        }
    }*/
    stage ('unit test') {
        steps {
            script {
                sh "mvn test"
            }
        }
    }
    stage ('sonar analysis'){
        steps {
            script {
                 withSonarQubeEnv('sonar') {
                  def SONAR_SCAN_HOME = tool 'sonar-scanner'
                  sh "${SONAR_SCAN_HOME}/bin/sonar-scanner -Dsonar.projectKey=hello-world"
              }
            }
        }
    }
  }
}


