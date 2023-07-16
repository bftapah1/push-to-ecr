pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t marecl:latest .'
            }
        }

        stage('Login to ECR') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Demo-ecs', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh 'eval $(aws ecr get-login --no-include-email --region us-east-2)'
                }
            }
        }

        stage('Push to ECR') {
            steps {
                sh 'docker tag marecl:latest 176039391845.dkr.ecr.us-east-2.amazonaws.com/marecl:latest'
                sh 'docker push 176039391845.dkr.ecr.us-east-2.amazonaws.com/marecl:latest'
            }
        }

        stage('Logout from ECR') {
            steps {
                sh 'docker logout 176039391845.dkr.ecr.us-east-2.amazonaws.com'
            }
        }
    }
}
