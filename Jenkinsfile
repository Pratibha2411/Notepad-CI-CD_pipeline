pipeline {
    agent { label 'node-agent' }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('notepadapp-dockerhub')
        }
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
        stage('Login'){
        steps{
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        }
        }
        stage('Push image on DockerHub'){
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
        post {
        always {
        sh 'docker logout'
        }
        }
}
