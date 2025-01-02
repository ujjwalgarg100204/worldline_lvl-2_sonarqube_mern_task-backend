pipeline {
    agent any

    environment {
        SONAR_AUTH_TOKEN = credentials('mern-stack-task_backend_sonar-token')
    }

    stages {
        stage('Install Dependencies') {
            steps {
                nodejs(nodeJSInstallationName: 'Default') {
                    sh 'npm install'
                }
            }
        }

        stage('SonarQube') {
            steps { 
                def scannerHome = tool 'SonarScanner 6.x';
                withSonarQubeEnv('LocalSonarQube') {
                      sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=mern-stack-task_backend \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://your-sonarqube-server-url \
                        -Dsonar.token=${SONAR_AUTH_TOKEN}
                        """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
                }
            }
        }
    }
}
