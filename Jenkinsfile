pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                nodejs(nodeJSInstallationName: 'Default') {
                    sh 'npm install'
                }
            }
        }
    }
}
