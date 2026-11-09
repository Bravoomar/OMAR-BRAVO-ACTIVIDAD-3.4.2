pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Compilando y preparando el entorno del proyecto...'
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando pruebas unitarias...'
            }
        }

        stage('Generate Documentation') {
            steps {
                echo 'Generando documentación con Doxygen...'
                sh 'doxygen Doxyfile'
            }
        }

        stage('Version Control') {
            steps {
                echo 'Actualizando repositorio con la documentación generada...'
                sh '''
                    git config user.name "Jenkins CI"
                    git config user.email "jenkins@build.local"
                    git add docs/
                    git diff --quiet && git diff --staged --quiet || git commit -m "docs: actualización automática de documentación Doxygen [skip ci]"
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Desplegando la aplicación en el entorno de prueba...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline ejecutado exitosamente. Documentación actualizada.'
        }
        failure {
            echo 'El pipeline ha fallado en alguna de sus etapas.'
        }
    }
}