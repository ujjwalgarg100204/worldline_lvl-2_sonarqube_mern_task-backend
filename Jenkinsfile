pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ujjwalgarg100204/worldline_lvl-2_sonarqube_mern_task-backend'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
    }
}
