# nodeApp-notepad-CI/CD

Run these commands:

`sudo apt install nodejs`
`sudo apt install npm`
`npm install`
`node app.js`

Steps for CI/CD:
  
  Create AWS EC2 instance
  sudo apt update
  sudo apt install openjdk-11-jre
  java -version
  curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
  sudo apt-get update 
  sudo apt-get install jenkins
  sudo systemctl enable jenkins
  sudo systemctl start jenkins
  sudo systemctl status jenkins
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  
  sudo apt install docker.io
Dockerfile:
  FROM node:12.2.0-alpine
  WORKDIR app
  COPY . .
  RUN npm install
  EXPOSE 8000
  CMD ["node","app.js"]

  docker build . -t node-app
  sudo usermod -a -G docker $USER
  docker run -d --name node-todo-app -p 8000:8000 todo-node-app
  
  __________________________________

Got to jenkins job:
  Execute shell 
  docker build . -t node-app-todo
  docker run -d --name node-app-container -p 8000:8000 node-app-todo


