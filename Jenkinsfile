pipeline {
    agent any

    // Parameters & Conditional Logic
    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: true, description: 'Should we deploy?')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test in Parallel') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests...'
                        sh 'sleep 5'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                        sh 'sleep 5'
                    }
                }
            }
        }

        // Archiving Artifacts
        stage('Test Results') {
            steps {
                sh 'echo "All tests passed!" > results.txt'
                archiveArtifacts artifacts: 'results.txt', fingerprint: true
            }
        }

        // Manual Approval before Deploy
        stage('Approval') {
            steps {
                input message: "Do you want to proceed with deployment?", ok: "Yes, Deploy"
            }
        }

        // Deploy (conditional with parameter)
        stage('Deploy') {
            when {
                expression { return params.RUN_DEPLOY }
            }
            steps {
                echo 'Deploying application...'
            }
        }
    }

    // Post actions
    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs!'
        }
        always {
            echo 'Pipeline completed (success or failure).'
        }
    }
}
