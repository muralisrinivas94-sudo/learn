pipeline {
  agent any

  stages {

    stage('Checkout Code') {
      steps {
        git 'https://github.com/muralisrinivas94-sudo/learn.git'
      }
    }

    stage('Run Python App') {
      steps {
        sh '''
        python3 --version
        python3 app.py &
        sleep 5
        curl localhost:5000 || true
        '''
      }
    }
  }
}
