pipeline {
     agent {
          label 'jenkins-agent'
        }
     tools {
          maven 'maven'
     }
     stages {
       stage ('test') {
          steps {
               script {
                    sh "mvn test"
               }
            }
         }
      stage ('sonarqube analasis') {
        steps {
          scrpit{
               def SONAR_SCANNER_HOME = tool 'sonar-scanner'
               sh  "$(SONAR-
     agent {
          label 'jenkins-agent'
        }
     tools {
          maven 'maven'
     }
     stages {
       stage ('test') {
          steps {
               script {
                    sh "mvn test"
               }
            }
         }
       stage ('build') {
          steps {
              script{
                   sh "mvn package"
              }
          }
       }
          }
        }
      }
       stage ('build') {
          steps {
              script{
                   sh "mvn package"
              }
          }
       }
  }  
}
