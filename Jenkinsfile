pipeline {
    agent any  // Ejecutar en cualquier agente disponible

    environment {
        // Variables de entorno si es necesario
        BRANCH_NAME = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Realiza un checkout de la rama 'feature'
                    checkout scm: [
                        $class: 'GitSCM', 
                        branches: [[name: "*/${env.BRANCH_NAME}"]], 
                        userRemoteConfigs: [[url: 'https://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@github.com/OierBaigo/react19.git']]
                    ]
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        stage('Ejecutar Tests con Cobertura') {
            steps {
                sh 'npm test -- --coverage --pashWithNoTest'
            }
        }

        stage('Publicar Resultados de Cobertura') {
            steps {
                sh 'npm run coverage-report'  
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }

        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
