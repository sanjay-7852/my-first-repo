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
                sudo docker build -t new-repo .
                
                '''
            }
        }
        stage('s3 bucket') {
            steps {
                echo 'Uploading Docker image to S3...'
                sh '''
                sudo aws s3 cp /var/lib/jenkins/workspace/admin@2/my-docker-image.tar s3://jenkinssss/jenkins/my-docker-image.tar --region ap-south-1
                '''
            }
        }
        
    }
}
