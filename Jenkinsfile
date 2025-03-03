pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.image('node:18-alpine').inside {
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
            }
        }
        stage('Test') {
            steps {
                script {
                    // Run npm test inside the container
                    docker.image('node:18-alpine').inside {
                        sh 'npm test'
                    }
                    // Now, check for the existence of build/index.html in the workspace
                    if (fileExists('build/index.html')) {
                        echo "Test Pass: index.html found in build directory."
                    } else {
                        error "Test Failed: index.html NOT found in build directory."
                    }
                }
            }
        }
        post {
            always {
                junit 'test-results/junit.xml'
            }
        }
    }
}
