pipeline {
    agent any
    tools {
        nodejs "nodejs"
    }
    environment {
        CI = 'true'
        GITHUB_TOKEN = credentials('GITHUB_TOKEN') // Stored from Jenkins Credentials
    }
    parameters {
        string defaultValue: 'main', description: 'git branch to build', name: 'DEPLOY_BRANCH'
    }
    stages {
        stage("Git Checkout") {
            steps {
                git url:"https://github.com/ToanDieu/deploy-gitpages",branch:"${params.DEPLOY_BRANCH}"
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
                bat "npm i -g gh-pages"
                bat "gh-pages -d build -b gh-pages -r https://%GITHUB_TOKEN%@github.com/ToanDieu/deploy-gitpages.git"
            }
        }
    }
}