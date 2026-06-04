pipeline {
agent any

```
environment {
    IMAGE_NAME = "myapp"
    CONTAINER_NAME = "myapp-container"
}

stages {

    stage('Build Docker Image') {
        steps {
            sh """
            docker build -t ${IMAGE_NAME}:latest .
            """
        }
    }

    stage('Stop Existing Container') {
        steps {
            sh """
            docker stop ${CONTAINER_NAME} || true
            docker rm ${CONTAINER_NAME} || true
            """
        }
    }

    stage('Run Container') {
        steps {
            sh """
            docker run -d \
            --name ${CONTAINER_NAME} \
            -p 80:80 \
            ${IMAGE_NAME}:latest
            """
        }
    }

}

post {
    success {
        echo 'Application deployed successfully!'
    }

    failure {
        echo 'Pipeline failed!'
    }
}
```

}
