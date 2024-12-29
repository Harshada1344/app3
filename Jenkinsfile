pipeline {
    agent any
    stages {
        
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Harshada1344/app3.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh "/usr/local/bin/docker image build -t harshada437/app3 ."
            }
        }
        
        stage("Push docker image") {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_HUB_TOKEN', variable: 'DOCKER_HUB_TOKEN')]) {
                    sh "echo dckr_pat_WH-CqdmWs2bLAioMe5YyUf7C-bQ | /usr/local/bin/docker login -u harshada437 --password-stdin"
                    sh "/usr/local/bin/docker image push harshada437/app3"
                }
            }
        }
        
        stage("Deploy docker service") {
            steps {
                sh "/usr/local/bin/docker service rm webservice"
                sh "/usr/local/bin/docker service create --name webservice -p 8000:80 --replicas 2 harshada437/app3"
            }
        }
        
    }
}
