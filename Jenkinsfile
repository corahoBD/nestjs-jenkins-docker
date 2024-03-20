pipeline {
    agent any // Sử dụng bất kỳ agent nào có sẵn

    environment {
        // Thiết lập biến môi trường cho nhánh
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
        stage('Build') {
            steps {
                // Đảm bảo rằng Node.js và npm đã được cài đặt trên Jenkins agent hoặc máy chủ
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        // Thêm các giai đoạn khác như 'Deploy' tùy vào nhu cầu của bạn
    }

    post {
        always {
            echo 'Cleaning up...'
            // Lệnh dọn dẹp nếu cần
        }
    }
}
