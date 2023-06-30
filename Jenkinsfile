pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/anasshwi/docker-nginx', branch: 'master')
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t anasshwi/docker-nginx:$BUILD_ID .'
      }
    }

    stage('run & test') {
      steps {
        sh 'docker run -itd --name docker-nginx -p 80:80 anasshwi/docker-nginx :$BUILD_ID'
        sleep 3
        sh 'curl localhost:8080'
        sh 'docker stop docker-nginx && docker rm docker-nginx '
      }
    }

    stage('push') {
      steps {
        sh 'docker login -u anasshwi -p Anas123456'
        sh 'docker tag anasshwi/docker-nginx :$BUILD_ID anasshwi/docker-nginx :latest'
        sh 'docker push anasshwi/docker-nginx:latest'
        sh 'docker push anasshwi/docker-nginx :$BUILD_ID'
      }
    }

  }
}