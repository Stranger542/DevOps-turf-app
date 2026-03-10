pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }
        stage('Lint/Test') {
            steps {
                echo 'Running basic checks...'
                // For a simple HTML site, we just check if files exist
                sh 'ls -la'
            }
        }
        stage('Build/Archive') {
            steps {
                echo 'Archiving build artifacts...'
                archiveArtifacts artifacts: '*.html, *.css, *.js', fingerprint: true
            }
        }
    }
}
