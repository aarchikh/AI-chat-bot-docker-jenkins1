pipeline {
 agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', poll: false, url: 'https://github.com/aarchikh/AI-chat-bot-docker-jenkins1.git'
            }
        }

        stage('Build and Push Images') {
            steps {
                script {
                    sh 'docker build -t aarchikh07/react-app1 .'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'ay_pass', usernameVariable: 'ay_user')]) {
                        sh 'docker login -u $ay_user -p $ay_pass'
                        sh 'docker push aarchikh07/react-app1 '
                    }
                }
            }
        }

        stage('Deploy Services') {
            steps {
                script {
                    sh 'docker rm -f  react-app4'
                    sh 'docker run -d --name my-react-app4 -p 1187:80 aarchikh07/react-app1'
                }
            }
        }
        
        stage('Post Deployment Testing') {
            steps {
                script {
                    sh 'curl -I http://localhost:1187'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
