pipeline{
     agent any
     tools
       {
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
