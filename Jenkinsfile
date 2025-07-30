pipeline {
     agent {
          docker {
            image 'maven:3.8.4-jdk-11' // Docker image to use
            args '-v /root/.m2:/root/.m2' // Optional: additional Docker args
        }
     }
     stages {
       stage ('test') {
          steps {
               script {
                    sh "mvn test"
               }
          }
     }
     stage ('sonar') {
       agent {
          docker {
            image 'joebaird/sonarscanner' // Docker image to use
        }
     }
     steps {
          script {
               sh "sonar-scanner --version"
          }
      }
     }
     stage ('build') {
       steps {
            script {
                 sh "mvn package"
                 archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
       }
     }
   }
}
