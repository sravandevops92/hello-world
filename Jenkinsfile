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
       stage ('build') {
          steps {
              script{
                   sh "mven package"
              }
          }
       }
  }  
}
