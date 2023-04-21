pipeline {
    agent {label 'agent'}
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/yogendra-kokamkar/ChatGPT-CICD.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'sudo docker build . -t yogendrakokamkar/chatgpt'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'DockerPassword', usernameVariable: 'DockerUser')]) {
        	     sh "sudo docker login -u ${env.DockerUser} -p ${env.DockerPassword}"
                 sh 'sudo docker push yogendrakokamkar/chatgpt'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "sudo docker-compose down"
                sh "sudo docker-compose up -d --force-recreate --no-deps --build web"
            }
        }
    }
}