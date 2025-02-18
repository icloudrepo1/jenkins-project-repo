pipeline {
    agent any

    stages {
        stage('code clone') {
            steps {
                echo "code cloning hogya repo se"
                git url: "https://github.com/cloudrepo1/jenkins-pro.git"
            }
        }
        stage('code build') {
            steps {
                echo "code build v karliye"
                sh "docker build . -t mywebappimg:latest"
            }
        }

        ///// if any error during code build :- install docker , sudo usermod -aG docker jenkins , sudo systemctl restart jenkins ( again build now )
        
        stage('code test') {
            steps {
                echo "code testing hogya"
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag mywebappimg ${env.dockerHubUser}/mywebappimg:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/mywebappimg:latest"
                }
            }
        }
        stage("deploy"){
            steps {
                echo "deploying the container"
                sh "docker-compose down && docker-compose up -d"
    }
}
