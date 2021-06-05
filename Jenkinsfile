node('nodejs') {
    stage('checkout') {
        git branch: 'main',
        url: 'https://github.com/leodomel/do400-pipelines-control'
    }
    stage('Backend Tests') {
        sh 'node ./backend/test.js'
    }
    stage('Frontend Tests') {
        sh 'node ./frontend/test.js'
    }
}