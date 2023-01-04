pipeline {
    agent {
        docker {
            image 'node:16'
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
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan)'
                sh './jenkins/scripts/deliver.sh'
                sh 'sleep 1m'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
