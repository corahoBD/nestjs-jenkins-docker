pipeline {
    agent {
        // Sử dụng Docker image mà bạn muốn để chạy pipeline, thí dụ như `node:14-alpine`
        docker { 
            image 'node:14-alpine'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        // Thiết lập biến môi trường cho nhánh
        BRANCH_NAME = 'main'
    }

    stages {
        stage('Prepare') {
            steps {
                // In thông tin nhánh được sử dụng
                script {
                    echo "Using branch: ${BRANCH_NAME}"
                }
            }
        }
        stage('Cloning Git') {
            steps {
                // Sử dụng lệnh `checkout` để clone repository
                checkout([$class: 'GitSCM', branches: [[name: "*/${BRANCH_NAME}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GithubCredential', url: 'https://github.com/corahoBD/nestjs-jenkins-docker.git']]])
                echo "Clone git repository from branch: ${BRANCH_NAME}"
            }
        }
        stage('Build') {
            steps {
                // Sử dụng Docker để chạy lệnh build, thí dụ cho một project Node.js
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                // Chạy lệnh test nếu có
                sh 'npm test'
            }
        }
        // Thêm các giai đoạn khác như 'Deploy' tùy vào nhu cầu của bạn
    }

    // Cấu hình để dọn dẹp sau khi pipeline chạy xong
    post {
        always {
            echo 'Cleaning up...'
            // Lệnh dọn dẹp nếu cần
        }
    }
}
