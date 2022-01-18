pipeline{
    agent any
    stages{

        stage('Build Docker Image') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'MMT-Dockerhub', url: 'https://github.com/nddat1811/flask.git']]])
                    bat 'docker build -t nddat1811/19127355_19127596 .'
                }
            }
        }
        stage('Docker login ') {
            steps {
                script {
                    bat 'docker login -u nddat1811 -p fe802ad7-c45a-4ab9-86f0-27460cde7c22'
                }
            }
        }
        stage('Deploy Docker Push') {
            steps {
                script {
                    bat 'docker push nddat1811/19127355_19127596:latest'
                }
            }
        }
        stage('Jenkins deploy the app to docker container') {
            steps {
                bat "docker compose up"
            }
        }
    }
    
   post {
        always{
            bat 'docker logout'
        }
    }

}
