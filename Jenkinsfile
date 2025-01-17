pipeline {
    agent { label 'ub1' }

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps {
                sh(script: 'sudo docker compose build')
            }
        }
    }
}