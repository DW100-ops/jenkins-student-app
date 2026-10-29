pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'python3 -m py_compile app.py test_app.py'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m unittest -v test_app'
            }
        }
        stage('Package') {
            steps {
                sh '''
                tar -czf app-package.tar.gz \
                app.py test_app.py
                '''
                archiveArtifacts artifacts: 'app-package.tar.gz'
            }
        }
    }
    post {
        success {
            echo 'CI pipeline completed successfully'
        }
        failure {
            echo 'CI pipeline failed. Check Console Output.'
        }
        always {
            echo 'Pipeline execution finished'
        }
    }
}