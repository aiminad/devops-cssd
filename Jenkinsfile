pipeline {
    agent any
    
    stages {

        stage('Build') {
            steps {
                script {
                    sh 'apt-get update'
                    sh 'apt-get upgrade -y'

                    sh '''
                       
                        docker compose version
                        '''
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {

                    sh 'apt-get update'
                    sh 'apt-get upgrade -y'
                    sh '''
                        docker compose version
                        docker compose up -d
                        '''

                    sh 'apt-get install -y python3 python3-venv python3-pip'

                    sh '''
                        python3 -m venv .venv
                        . .venv/bin/activate
                        pip install pytest selenium

                        sleep 15
                        python test_devopstest.py
                        '''
                }
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                echo "Deployment started..."
                docker run -d -p 81:80 my-app
                echo "Application deployed successfully and running on port 81!"
                '''
            }
        }
    }
}
