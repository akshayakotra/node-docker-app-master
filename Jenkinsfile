pipeline {
    agent any

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/akshayakotra/node-docker-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t node-docker-app:${BUILD_NUMBER} .
                docker tag node-docker-app:${BUILD_NUMBER} akshayakotra/node-docker-app:${BUILD_NUMBER}
                '''
            }
        }

        // stage('Push Docker Image') {
        //     steps {
        //         sh 'docker push laxmi916/node-docker-app:${BUILD_NUMBER}'
        //     }
        // }
        
        stage('Create container') {
            steps {
                sh 'docker run -d -p 3000:8080 akshayakotra/node-docker-app:${BUILD_NUMBER}'
            }
        }



    }
}
