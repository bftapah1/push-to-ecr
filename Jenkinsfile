pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t bftimg:latest .'
            }
        }

        stage('Login to ECR') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Demo-ecs', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh 'eval $(aws ecr get-login --no-include-email --region us-east-1)'
                }
            }
        }

        stage('Push to ECR') {
            steps {
                sh 'docker tag bftimg:latest 743856502949.dkr.ecr.us-east-1.amazonaws.com/bftapah1'
                sh 'docker push 743856502949.dkr.ecr.us-east-1.amazonaws.com/bftapah1'
            }
        }

        stage('Logout from ECR') {
            steps {
                sh 'docker logout 743856502949.dkr.ecr.us-east-1.amazonaws.com/bftapah1'
            }
        }
    }
}
