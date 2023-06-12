pipeline{
    agent any
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/prabhjot219/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t pk219/node-todo:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId:'docker-hub',passwordVariable:'dockerhubpassword',usernameVariable:'dockerhubusername')]){
                    sh "docker login -u ${env.dockerhubusername} -p ${env.dockerhubpassword}"
                    sh 'docker image push pk219/node-todo:latest'
                }
            }
        }
        stage('Test'){
            steps{
                echo "Testing from github"
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down"
                sh "docker-compose up -d --force-recreate"
            }
        }
    }
}
