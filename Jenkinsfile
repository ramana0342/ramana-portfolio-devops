pipeline {
agent any


stages {
    stage('Clone') {
        steps {
            git 'https://github.com/ramana0342/ramana-portfolio-devops.git'
        }
    }

    stage('Build Backend Image') {
        steps {
            dir('back-end') {
                sh 'docker build -t portfolio-backend .'
            }
        }
    }

    stage('Deploy Backend') {
        steps {
            sh 'docker stop portfolio-backend-container || true'
            sh 'docker rm portfolio-backend-container || true'

            sh '''
            docker run -d \
            --name portfolio-backend-container \
            -p 5000:5000 \
            --env-file /home/ec2-user/ramana-portfolio-devops/back-end/.env \
            portfolio-backend
            '''
        }
    }

    stage('Build Frontend Image') {
        steps {
            dir('front-end') {
                sh 'docker build -t portfolio-frontend .'
            }
        }
    }

    stage('Deploy Frontend') {
        steps {
            sh 'docker stop portfolio-frontend-container || true'
            sh 'docker rm portfolio-frontend-container || true'

            sh '''
            docker run -d \
            --name portfolio-frontend-container \
            -p 3000:3000 \
            portfolio-frontend
            '''
        }
    }
}


}
