pipeline {
    agent any

    stages {
        stage('git clone') {
            steps {
               git 'https://github.com/manoharej/hello-world.git'
            }
        }
        
        stage('Maven install') {
            steps {
               sh '/opt/maven/bin/mvn clean test '
            }
        }
        stage('Maven build package') {
            steps {
               sh '/opt/maven/bin/mvn clean package '
            }
        }
        
       
        stage('Build docker file artifact') {
            steps {
                sh 'docker build -t testimage -f /opt/Dockerfile .'
            }
        }
        stage('Docker stop the running or existing container') {
            steps {
                sh 'docker stop testapp'
                sh 'docker rm testapp'
            }
        }
        
        stage('Doker run') {
            steps {
                sh 'docker run -d --name testapp -p 8090:8080 testimage'
            }
        }
    }
}
