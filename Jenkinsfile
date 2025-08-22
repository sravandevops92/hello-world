pipeline {
     agent {
          label 'jenkins-agent'
        }
     tool {
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
}  
