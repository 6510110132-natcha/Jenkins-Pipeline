pipeline {
    agent any

    // Parameters & Conditional Logic
    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: true, description: 'Should we deploy?')
        choice(name: 'ENV', choices: ['dev', 'staging', 'prod'], description: 'Select environment')
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
                    when {
                        expression { currentBuild.currentResult == null || currentBuild.currentResult == 'SUCCESS' }
                    }
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
                stage('Simulate Testing on Linux') {
                    steps {
                        echo 'Simulating tests on Linux...'
                    }
                }
                stage('Simulate Testing on Windows') {
                    steps {
                        echo 'Simulating tests on Windows...'
                    }
                }
            }
        }

        stage('Test Results') {
            steps {
                sh 'echo "All tests passed!" > results.txt'
                archiveArtifacts artifacts: 'results.txt', fingerprint: true
            }
        }

        stage('Approval') {
            options {
                timeout(time: 2, unit: 'MINUTES')
            }
            steps {
                input message: "Do you want to proceed with deployment?", ok: "Yes, Deploy"
            }
        }

        stage('Deploy') {
            when {
                expression { return params.RUN_DEPLOY }
            }
            steps {
                echo "Deploying application to environment: ${params.ENV}"
            }
        }
    }

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
