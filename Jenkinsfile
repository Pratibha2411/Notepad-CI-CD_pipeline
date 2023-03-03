pipeline {
    agent { label 'node-agent' }
    
    stages{
        stage('Code'){
            steps{ 
                git url: 'https://github.com/Pratibha2411/Notepad-CI-CD_pipeline.git', branch: 'main' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t notepad/node-todoapp-test:latest'
            }
        }
        stage('Push image on Hub'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push notepad/node-todo-test:latest'
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
