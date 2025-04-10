pipeline {
    agent any
    tools {
        nodejs "nodejs"
    }
    environment {
        CI = 'true'
    }
    stages {
        stage("Git Checkout") {
            steps {
                git url:"https://github.com/ToanDieu/deploy-gitpages",branch:"main"
            }
        }
        stage("NPM Install") {
            steps {
                bat "npm install"
            }
        }
        stage("Node Build") {
            steps {
                bat 'rmdir /s /q build'
                bat "npm run build --verbose"
            }
        }
        stage("Deploy Git pages") {
            steps {
                bat "git config --global user.email 'dieutoanktdl@gmail.com'"
                bat "git config --global user.name 'toan dieu'"
                bat "npm run deploy --verbose"
            }
        }
    }
}