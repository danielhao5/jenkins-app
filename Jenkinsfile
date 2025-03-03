pipeline {
    agent any 

    stages {
        stage ('Build') {
            //agent {
            //    docker {
            //        image 'node:18-apline'
            //         reuseNode true
            //    }
            steps {
                script {
                    docker.image('node:18-alpine').inside {
                        sh '''
                        ls -la
                        node --version
                        npm --version
                        npm ci
                        npm run build
                        echo 'build is Done. '
                        ls -la
                    '''
                    }
                }
            }
        }
    }



