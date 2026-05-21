pipeline {

    agent {
        label 'kapish'
    }

    tools {
        maven 'my-maven'
        //dockerTool 'my-docker'
    }
    environment {
        calcwebappmvn = 'calcwebappmvn'
    }

    stages {

        stage('Git Checkout') {
            steps {

                git url: 'https://github.com/Kapish0879/calcwebappmvn.git'

                echo "Code Checked-out Successfully!!"

                sh 'ls -la'
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

                sh 'docker build -t $calcwebappmvn:$BUILD_NUMBER .'

                echo "Docker Image Built Successfully!!"

                sh 'docker images'
            }
        }
        //pushing image to aws ecr
        stage('Docker Push') {
            steps {

                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 964742912902.dkr.ecr.us-east-1.amazonaws.com'

                sh 'docker tag $calcwebappmvn:$BUILD_NUMBER 964742912902.dkr.ecr.us-east-1.amazonaws.com/dev/project:$BUILD_NUMBER'

                sh 'docker push 964742912902.dkr.ecr.us-east-1.amazonaws.com/dev/project:$BUILD_NUMBER'

                echo "Docker Image Pushed to AWS ECR Successfully!!"
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
