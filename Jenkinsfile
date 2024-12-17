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
        stage('s3-push') {
            steps {
                echo 'Uploading Docker image to ecr service...'
                sh '''
                sudo aws s3 cp /var/lib/jenkins/workspace/admin/dockerfile s3://jenkinssss/jenkins/dockerfile --region ap-south-1
                '''
            }
        }
        
    }
}
