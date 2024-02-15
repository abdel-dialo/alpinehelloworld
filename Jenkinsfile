pipeline {
    agent any

    environment {
        IMAGE_NAME='alpinehelloworld'
        TAG_NAME='latest'
    }

    stages {
        stage('Build') {
            
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG_NAME .'
                sh 'docker rm -f  $IMAGE_NAME'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run -dti  --name $IMAGE_NAME -e PORT=5000  -p 80:5000  $IMAGE_NAME:$TAG_NAME'
                sh 'sleep 5'
                sh 'apk update && apk add curl'
                sh 'curl -I http://172.17.0.1'
        
            }
        }
        
    }
}
