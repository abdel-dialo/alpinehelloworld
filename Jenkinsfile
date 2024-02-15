pipeline {
    agent any

    environment {
        IMAGE_NAME="${PARAM_IMAGE_NAME}"
        TAG_NAME="${PARAM_TAG_NAME}"
        DOCKERHUB_ID="${PARAM_DOCKERHUB_ID}"
        //DOCKERHUB_PW="${DOCKERHUB_PW}"
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
                sh 'curl -I http://172.17.0.1'
        
            }
        }
        stage('clear container') {
            steps {
                sh '''
                 docker stop $IMAGE_NAME
                 docker rm $IMAGE_NAME
                '''       
            }
        }
        stage('Release') {
            steps {
                sh '''
                echo $DOCKERHUB_PW | docker login -u $DOCKERHUB_ID --password-stdin
                docker push  $IMAGE_NAME:$TAG_NAME
                '''
        
            }
        }
        
    }
}
