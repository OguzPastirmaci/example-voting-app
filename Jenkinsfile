pipeline {
  agent {
    node {
      label 'ubuntu-1604-aufs-stable'
    }
  }
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t iad.ocir.io/intmahesht/credit-suisse-demo/example-voting-app_result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t iad.ocir.io/intmahesht/credit-suisse-demo/example-voting-app_vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t iad.ocir.io/intmahesht/credit-suisse-demo/example-voting-app_worker ./worker'
      }
    }
    stage('Push result image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'') {
          sh 'docker push iad.ocir.io/intmahesht/credit-suisse-demo/example-voting-app_result'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'') {
          sh 'docker push iad.ocir.io/intmahesht/credit-suisse-demo/example-voting-app_worker'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'') {
          sh 'docker push iad.ocir.io/intmahesht/credit-suisse-demo/example-voting-app_worker'
        }
      }
    }
  }
}
