pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'mvn -B clean compile'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn -B test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy') {
            steps {
                bat 'mvn -B package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar'
                echo 'Aplicación desplegada correctamente'
            }
        }
    }

    post {
        success { echo 'RESULTADO: todo salió bien' }
        failure { echo 'RESULTADO: el pipeline falló' }
    }
}