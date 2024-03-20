pipeline {
    agent any
    environment {
        BRANCH_NAME = 'main'
    }

    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "*/${BRANCH_NAME}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GithubCredential', url: 'https://github.com/corahoBD/nestjs-jenkins-docker.git']]])
                echo "Clone git repository from branch: ${BRANCH_NAME}"
            }
        }
    }
}
