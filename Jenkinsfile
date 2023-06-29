pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/anasshwi/nginx', branch: 'master', changelog: true, poll: true)
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t nginx :$BUILD_ID '
      }
    }

    stage('run & test') {
      steps {
        sh 'docker run --name nginx -d -p 80:80 nginx :$BUILD_ID'
        sleep 3
        sh 'curl localhost:8080'
        sh 'docker stop nginx && docker rm nginx'
      }
    }

    stage('push') {
      steps {
        sh 'docker tag nginx :$BUILD_ID anasshwi/nginx :$BUILD_ID'
        sh 'docker login -u anasshwi -p Anas123456'
        sh 'docker push anasshwi/nginx :$BUILD_ID'
      }
    }

  }
}