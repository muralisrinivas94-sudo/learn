pipeline {
  agent {
    kubernetes {
      label 'kaniko-build'
      defaultContainer 'kaniko'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:

  - name: kaniko
    image: gcr.io/kaniko-project/executor:latest
    command:
    - cat
    tty: true
    volumeMounts:
    - name: docker-config
      mountPath: /kaniko/.docker

  volumes:
  - name: docker-config
    secret:
      secretName: dockerhub-secret
"""
    }
  }

  environment {
    IMAGE = "docker.io/murali1327/test"
    TAG   = "${BUILD_NUMBER}"
  }

  stages {

    stage('Checkout from GitHub') {
      steps {
        checkout scm
      }
    }

    stage('Build & Push Image using Kaniko') {
      steps {
        container('kaniko') {
          sh """
          /kaniko/executor \
            --context $WORKSPACE \
            --dockerfile $WORKSPACE/Dockerfile \
            --destination $IMAGE:$TAG \
            --destination $IMAGE:latest
          """
        }
      }
    }
  }
}
