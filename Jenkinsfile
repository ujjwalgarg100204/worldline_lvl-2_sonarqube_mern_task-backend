pipeline {
    agent any

    environment {
        SONARQUBE_SCANNER_HOME = tool 'SonarScanner 6.x'
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
                withSonarQubeEnv('LocalSonarQube') {
                      sh """
                        ${SONARQUBE_SCANNER_HOME}/bin/sonar-scanner \
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
