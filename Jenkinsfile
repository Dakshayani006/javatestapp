
pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "daksha006/train-schedule"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    app.inside {
                        sh 'echo Hello, World!'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                       }
                }
            }
        }
        stage('DeployToProduction') {
            steps {
                input 'Deploy to Dev Environment?'
                milestone(1)
                kubernetesDeploy(
                    credentialsType: 'KubeConfig',
                    kubeConfig: [path: '/var/lib/jenkins/.kube/config'],
                    configs: 'train-schedule-kube.yml',
                )
            }
        }

        stage('RollBack') {
          steps {
             script {

                sh 'kubectl set image deployment/test test=test:3 --record=true'
                sh 'kubectl rollout history deployment/test'
                sh 'kubectl rollout undo deployment/test --to-revision=14'
         }
       }
     }

    }
}
                                                                                                                  


