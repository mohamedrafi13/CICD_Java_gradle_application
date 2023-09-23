pipeline {
    agent any
    environment {
        VERSION = "${env.BUILD_ID}"
    }
    
    /*stages{
        stage("Sonar Quality Check"){
            agent {
                docker {
                    image 'openjdk:11'
                }
            }
             steps {
                script  {
                    withSonarQubeEnv(credentialsId: 'deekshithsn') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
                }
            }
        } */
        stages {
            stage('docker build & docker push'){
                steps{
                    script{
                        withCredentials([string(credentialsId: 'nexus-login', variable: 'nexusloginvariable')]) {
                        sh '''
                        docker build -t 172.31.40.82:8083/springapp:${VERSION} .
                        docker login -u admin -p $nexusloginvariable 172.31.40.82:8083
                        docker push 172.31.40.82:8083/springapp:${VERSION}
                        docker rmi 172.31.40.82:8083/springapp:${VERSION}
                        '''
                    }
                    
                }
            }
        }
        stage('Identifying misconfigs using datree in helm charts') {
            steps{
                script{
                    dir('kubernetes/') {
                        sh 'helm datree test myapp/'
                    }

                }
            }
        }
    }
    post {
		always {
			mail bcc: '', body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "${currentBuild.result} CI: Project name -> ${env.JOB_NAME}", to: "dhirafiayeshafi@gmail.com";  
		}
	}
} 
