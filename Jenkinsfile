pipeline {
    agent any

    stages {
        stage ('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Harshada1344/app3.git'
            }
        }
        stage ('docker login') {
            steps {
                sh 'dckr_pat_WH-CqdmWs2bLAioMe5YyUf7C-bQ | /usr/bin/docker login -u harshada437 --password-stdin'
            }
        }
        stage ('docker build image') {
            steps {
                sh '/usr/bin/docker image build -t harshada437/app3 .'
            }
        }
        stage ('docker push image') {
            steps {
                sh '/usr/bin/docker image push harshada437/app3'
            }
        }
        stage ('docker remove service') {
            steps {
                sh '/usr/bin/docker service rm webservice'
            }
        }
        stage ('docker create service') {
            steps {
                sh '/usr/bin/docker webservice create --name webservice -p 8000:80 --replicas 2 harshada437/app3'
            }
        }
    }
}
