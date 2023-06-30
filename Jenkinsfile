pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/anasshwi/nginx', branch: 'master')
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t anasshwi/nginx:${env.BUILD_NUMBER} .'
      }
    }

    stage('run & test') {
      steps {
        sh 'docker run -itd --name nginx -p 80:80 anasshwi/nginx :${env.BUILD_NUMBER}'
        sleep 3
        sh 'curl localhost:8080'
        sh 'docker stop nginx && docker rm nginx'
      }
    }

    stage('push') {
      steps {
        sh 'docker login -u anasshwi -p Anas123456'
        sh 'docker tag anasshwi/nginx :${env.BUILD_NUMBER} anasshwi/nginx :latest'
        sh 'docker push anasshwi/nginx:latest'
        sh 'docker push anasshwi/nginx :${env.BUILD_NUMBER}'
      }
    }

  }
}