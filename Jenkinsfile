pipeline {

    agent {
        label 'kapish'
    }

    tools {
        maven 'my-maven'
        //dockerTool 'my-docker'
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
