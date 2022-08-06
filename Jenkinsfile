pipeline {
    agent none
    stages {
        stage('dependencies') {
            steps {
                sh 'npm i'
            }
        }
        stage('cypress parallel tests') {
            environment {
                CYPRESS_RECORD_KEY = credentials('cypress-example-record-key')
                CYPRESS_PROJECT_ID = credentials('cypress-example-project-id')
                CYPRESS_trashAssetsBeforeRuns = 'false'
            }

            parallel {
                stage('machine 1') {
		    agent {
                    	docker { image 'node:16.13.1-alpine' }
		    }
                    steps {
			echo "Running build ${env.BUILD_ID}"
                        sh "npm run cy:ci"
                    }
                }

                stage('machine 2') {
                    agent {
			docker { image 'node:16.13.1-alpine' }
                    }
		    steps {
                        echo "Running build ${env.BUILD_ID}"
			sh "npm run cy:ci"
                    }
                }
            }
        }
    }
}
