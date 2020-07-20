pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
	stage('Docker Build') {
		steps {
			sh(script: "sudo docker images -a")
		}
	}
    }
}
