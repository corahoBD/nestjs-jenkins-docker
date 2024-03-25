pipeline {
    agent any

    environment {
        BRANCH_NAME = 'main'
    }

    tools {
        nodejs 'nodejs'
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
        // stage('Install NodeJS') {
        //     steps {
        //         sh 'curl -sL https://deb.nodesource.com/setup_18.x | bash -'
        //         sh 'apt-get install -y nodejs'
        //     }
        // }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh 'npm start'
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
