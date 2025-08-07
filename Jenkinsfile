pipeline {
    agent { 
        label 'agent'
        }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/PriyeshPandey07/Nodejs-cicd.git', branch: 'main' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t priyeshpandey07/nodejs-cicd:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push priyeshpandey07/nodejs-cicd:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}