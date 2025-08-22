pipeline {
     agent {
          label 'jenkins-agent'
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
