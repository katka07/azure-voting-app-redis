pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
	stage('Docker Build') {
		sh(script: "docker images -a")
	}
    }
}
