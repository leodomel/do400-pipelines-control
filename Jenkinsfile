pipeline {
    agent {
        node {
            label 'nodejs'
        }
    }
    parameters {
        booleanParam(name: "RUN_FRONTEND_TESTS", defaultValue: true)
    }
    stages {
        stage('Run Tests') {
            parallel {
                stage('Backend Tests') {
                    steps {
                        sh 'node ./backend/test.js'
                    }            
                }
                stage('Frontend Tests') {
                    when { expression { params.RUN_FRONTEND_TESTS } }
                    steps {
                        sh 'node ./frontend/test.js'
                    }
                }
            }
        }
        stage('Deploy in Homologation') {
            when {
                expression { env.GIT_BRANCH != 'origin/main' }
            }
            steps {
                echo 'Deploying in homologation...'
            }
        }
        stage('Deploy in Production') {
            when {
                expression { env.GIT_BRANCH == 'origin/main' }
                beforeInput true
            }
            input {
                message 'Deploy the application in Production?'
            }
            steps {
                echo 'Deploying in production...'
            }
        }
    }
}