pipeline {
    agent any

    environment {
        IMAGE_NAME='alpinehelloworld'
        TAG_NAME='latest'
        DOCKER_HUB_ACCESS = credentials('credentiel dockerhub')
    }

    stages {
        stage('Build') {
            
            steps {
                sh 'echo  $DOCKER_HUB_ACCESS '
                sh 'docker build -t $IMAGE_NAME:$TAG_NAME .'
                sh 'docker rm -f  $IMAGE_NAME'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run -dti  --name $IMAGE_NAME -e PORT=5000  -p 80:5000  $IMAGE_NAME:$TAG_NAME'
                sh 'sleep 5'
                sh 'curl -I http://172.17.0.1'
        
            }
        }
        stage('Release') {
            steps {
                sh 'docker run -dti  --name $IMAGE_NAME -e PORT=5000  -p 80:5000  $IMAGE_NAME:$TAG_NAME'
                sh 'sleep 5'
                sh 'curl -I http://172.17.0.1'
        
            }
        }
        
    }
}
