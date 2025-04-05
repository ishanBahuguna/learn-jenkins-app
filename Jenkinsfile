pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            // npm ci --> it is basically npm i(install dep) for CI server
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                /* test -f build/index.html checks if the file build/index.html exists.
                -f means "check if it's a regular file".
                If the file exists, the command succeeds (exit code 0), and the pipeline continues.
                If the file does not exist, it fails (non-zero exit code), and the pipeline stops or marks this stage as failed.*/
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
    }
}