pipeline {
    agent any

    stages {
        stage('git') {
            steps {
                git 'https://github.com/Pritam-Khergade/student-ui.git'
            }
        }
        stage('docker') {
            steps {
                sh '''
                sudo yum install docker -y
                sudo systemctl start docker
                sudo systemctl enable docker
                '''
            }
        }
        stage('build') {
            steps {
                sh '''
                sudo docker build -t docker .
                '''
            }
        }
        stage('s3 bucket') {
            steps {
                echo 'Uploading Docker image to S3...'
                sh '''
                sudo aws ecr get-login-password --region ap-south-1 | sudo docker login --username AWS --password-stdin 992382723829.dkr.ecr.ap-south-1.amazonaws.com
                sudo docker tag docker:latest 992382723829.dkr.ecr.ap-south-1.amazonaws.com/docker:latest
                sudo docker push 992382723829.dkr.ecr.ap-south-1.amazonaws.com/docker:latest
                '''
            }
        }
        
    }
}
