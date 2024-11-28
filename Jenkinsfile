pipeline {
    agent {
    docker {
        image 'docker:latest'  // Docker CLI and docker-compose included
        args '-v /var/run/docker.sock:/var/run/docker.sock'
    }
}

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Arijghrs/taskflowHR.git'
            }
        }

        stage('Build Backend') {
            steps {
                script {
                    sh 'docker-compose build backend'
                }
            }
        }

        stage('Start Services') {
            steps {
                script {
                    sh 'docker-compose up -d db'
                }
            }
        }

        stage('Run Backend Tests') {
            steps {
                script {
                    sh 'docker exec backend npm test'
                }
            }
        }

        stage('Teardown') {
            steps {
                script {
                    sh 'docker-compose down'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed."
        }
    }
}

