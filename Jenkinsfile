pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/deuxzeros69/projet-Devops.git'
            }
        }

        stage('Install Packages') {
            steps {
                sh '''
                sudo apt-get update -y
                sudo apt-get install -y net-tools iproute2 iputils-ping nano
                '''
            }
        }

        stage('Copy Site Files') {
            steps {
                sh '''
                sudo mkdir -p /var/www/html
                sudo cp -r * /var/www/html/
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                cd /var/www/html
                echo "FROM nginx:latest" | sudo tee Dockerfile
                echo "COPY . /usr/share/nginx/html" | sudo tee -a Dockerfile
                sudo docker build -t myapp .
                '''
            }
        }
    }
}
