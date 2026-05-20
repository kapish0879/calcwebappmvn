pipeline {

    agent {
        label 'kapish'
    }

    tools {
        maven 'my-maven'
        dockerTool 'my-docker'
    }

    stages {

        stage('Git Checkout') {
            steps {

                git url: 'https://github.com/Kapish0879/calcwebappmvn.git'

                echo "Code Checked-out Successfully!!"

                sh 'ls -la'
            }
        }

        stage('Install Docker') {
            steps {

                sh '''

                        sudo apt update

                        sudo apt install docker.io -y

                        sudo systemctl start docker

                        sudo systemctl enable docker

                        sudo groupadd docker || true

                        sudo usermod -aG docker jenkins

                        sudo chmod 777 /var/run/docker.sock
                        
                '''
            }
        }

        stage('Package') {
            steps {

                sh 'mvn clean'

                sh 'mvn package'

                echo "Maven Package Goal Executed Successfully!"
            }
        }

        stage('Docker Build') {
            steps {

                sh 'docker --version'

                sh 'docker images'

                sh 'docker build -t calcwebappmvn:v1 .'

                echo "Docker Image Built Successfully!!"

                sh 'docker images'
            }
        }
    }

    post {

        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
