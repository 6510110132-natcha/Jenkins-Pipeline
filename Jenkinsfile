 pipeline {
    agent any
//Parameters & Conditional Logic
    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: true, description: 'Should we deploy?')
    }
    stages {
        stage('Deploy') {
            when {
                expression { return params.RUN_DEPLOY }
            }
            steps {
                echo 'Deploying application...'
            }
        }
    }
//Parallel Stages
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
    }
//Archiving Artifacts
    stage('Test') {
    steps {
        sh 'echo "All tests passed!" > results.txt'
        archiveArtifacts artifacts: 'results.txt', fingerprint: true
    }
}

    
}
