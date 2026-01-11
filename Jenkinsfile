This is added line
pipeline {
   agent any
   environment {
       IMAGE_NAME = "jenkinsdemo:latest"
       CONTAINER_NAME = "jenkinsdemo"
   }
   stages {
       stage('Checkout Code') {
           steps {
               git branch: 'main',
                   url: 'https://github.com/vishnuvishalgn/JenkinsDemo.git'
           }
       }
       stage('Build Docker Image') {
           steps {
               sh '''
                 docker build -t ${IMAGE_NAME} .
               '''
           }
       }
       stage('Deploy Container') {
           steps {
               sh '''
                 docker stop ${CONTAINER_NAME} || true
                 docker rm ${CONTAINER_NAME} || true
                 docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${IMAGE_NAME}
               '''
           }
       }
   }
   post {
       success {
           echo "✅ CI/CD Pipeline completed successfully"
       }
       failure {
           echo "❌ CI/CD Pipeline failed"
       }
   }
}
