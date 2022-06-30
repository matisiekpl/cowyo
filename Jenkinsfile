pipeline {
    agent any
    parameters {
       booleanParam(name: 'SHOULD_PUBLISH', defaultValue: false, description: 'Should publish?')
   }
    stages {
        stage('Build') {
            steps {
                docker build -t cowyo:c$GIT_COMMIT .
            }
        }
        stage('Test') {
            steps {
                docker run --rm cowyo:c$GIT_COMMIT go test ./...
            }
        }
        stage('Deploy') {
            steps {
                docker build -t cowyo-runtime:c$GIT_COMMIT -f Dockerfile.multistage .
                docker rm -f cowyo-app || exit 0
                docker run -d --name cowyo-app -p 8050:8050 cowyo-runtime:c$GIT_COMMIT
                sleep 10
                curl 'http://localhost:8050/'
            }
        }
        stage('Publish') {
            when {
                expression { params.DEPLOY_TO_PRODUCTION }
            }
            steps {
                docker push cowyo-runtime:c$GIT_COMMIT
            }
        }
    }
}