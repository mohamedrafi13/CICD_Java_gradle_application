pipeline{
    agent any
    stages{
        stage("Sonar Quality Check"){
            agent {
                docker {
                    image 'openjdk:11'
                }
            }
        /*     steps {
                script  {
                    withSonarQubeEnv(credentialsId: 'deekshithsn') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
                }
            }
        } */
            
    }
}
   