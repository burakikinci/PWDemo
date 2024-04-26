pipeline {
    agent any
    stages {
        stage('Print Hello') {
            steps {
                echo("Hello World")
            }
        }
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/burakikinci/PWDemo.git']]])
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
                bat 'npx playwright install webkit'
                bat 'npx playwright install chromium'
                bat 'npx playwright install firefox'
            }
        }
        stage('Install Playwright and its Browsers') {
            steps {
                bat 'npm install --save-dev playwright'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npx playwright test'
            }
        }
        stage('Upload Playwright report') {
            steps {
                archiveArtifacts artifacts: 'playwright-report/**', fingerprint: true
            }
        }
    }
}