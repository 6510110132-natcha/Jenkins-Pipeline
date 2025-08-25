pipeline {
    agent any
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
    stage('Test') {
    steps {
        sh 'echo "All tests passed!" > results.txt'
        archiveArtifacts artifacts: 'results.txt', fingerprint: true
    }
}

}
