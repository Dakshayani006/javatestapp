
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t javatestapp:v3 .'
                sh 'kubectl create deployment java --image=javatestapp:v3'
              sh 'sudo kubectl expose deployment java --type=LoadBalancer --port=8080'
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

        stage('RollBack') {
          steps {
             script {
            
               
                sh 'kubectl rollout history deployment/java'
                sh 'kubectl rollout undo deployment/java --to-revision=14'
         }
    }
 }
}
}

