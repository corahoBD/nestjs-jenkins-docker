pipeline {
    agent any

    environment {
        BRANCH_NAME = 'main'
    }

    stages {
        stage('Prepare') {
            steps {
                script {
                    echo "Using branch: ${BRANCH_NAME}"
                }
            }
        }
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "*/${BRANCH_NAME}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GithubCredential', url: 'https://github.com/corahoBD/nestjs-jenkins-docker.git']]])
                echo "Clone git repository from branch: ${BRANCH_NAME}"
            }
        }
        stage('Install NodeJS') {
            script {
                if (sh(script: 'node --version', returnStatus: true) != 0) {
                    echo 'Node.js is not installed. Installing...'
                    sh 'curl -sL https://deb.nodesource.com/setup_14.x | bash -'
                    sh 'apt-get install -y nodejs'
                } else {
                    echo 'Node.js is already installed'
                }
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh 'npm run start:dev'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
        }
    }
}
