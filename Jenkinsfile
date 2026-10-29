pipeline {
    agent any

    parameters {
        string(name: 'BUILD_ENV', defaultValue: 'staging', description: 'Target deployment environment')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Toggle unit test execution')
    }

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
            when {
                expression { params.RUN_TESTS == true }
            }
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
            echo "Pipeline completed successfully for environment: ${params.BUILD_ENV}"
        }
        failure {
            echo 'CI pipeline failed. Check Console Output.'
        }
        always {
            echo 'Pipeline execution finished'
        }
    }
}