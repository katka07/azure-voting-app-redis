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
                sh(script: 'docker compose build')
            }
        }
        stage('Start App') {
            steps {
                sh(script: 'docker compose up -d')
            }
        }
        stage('Run Tests') {
            steps {
                sh(script: 'pytest ./tests/test_sample.py')
            }
            post {
                success {
                    echo "Tests passed :)"
                }
                failure {
                    echo "Tests failed :("
                }
            }
        }
        stage('Docker Push') {
            steps {
                echo "Running in $WORKSPACE"
                dir("$WORKSPACE/azure-vote") {
                    script {
                        //docker.withRegistry('', 'dockerhub')
                        def image = docker.build('katka05/voting-app:2025')
                        image.push()
                    }
                }
            }
        }
        stage('Analyze image') {
            steps {
                dir("$WORKSPACE")
                sh 'docker-scout cves katka05/voting-app:2025 --only-severity critical,high'
            }
        }
    }
    post {
        always {
            sh(script: 'docker compose down')
        }
    }
}