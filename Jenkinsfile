pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Prepare') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Prepare'
                dir('code/frontend') {
                    sh 'npm install'
                }
                echo 'Prepare backend'
                dir('code/backend') {
                    sh 'npm install'
                }
            }
        }
        stage('Build') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Build'     
                dir('code/frontend') {
                    sh 'npm build'
                }
                echo 'Prepare backend'
                dir('code/backend') {
                    sh 'npm build'
                }
            }
        }
        stage('Static Analysis') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Analyze' 
                dir('code/frontend') {
                    sh 'npm run lint'
                }
                echo 'Analyze backend'
                dir('code/backend') {
                    sh 'npm run lint'
                }
            }
        }
        stage('Unit Test') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Test'
                dir('code/frontend') {
                    sh 'npm run test'
                }
                echo 'Test backend'
                dir('code/backend') {
                    sh 'npm run test'
                }
            }
        }
        stage('e2e Test') {
            steps {             
                echo 'e2e Test'
            }
            post {
                always {
                    echo 'Cleanup'
                }
            }
        }
        stage('Deploy') {
            steps {                
                echo 'Deploy'
            }
        }
    }
}
