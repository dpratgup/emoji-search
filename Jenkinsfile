pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    environment { 
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'set -x'
                sh 'npm test'
            }
        }
        stage('Deliver') { 
            steps {
                sh 'set -x'
                sh 'npm run build'
                sh 'set +x'
                sh 'set -x'
                sh 'npm start &'
                sh 'sleep 1'
                sh 'echo $! > .pidfile'
                sh 'set +x'
            }
        }
    }
}
