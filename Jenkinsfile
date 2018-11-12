

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t javatestapp1:v2 .'
                sh 'kubectl create deployment testing --image=javatestapp1:v2'
              sh 'sudo kubectl expose deployment testing --type=LoadBalancer --port=8080'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
  }
}
