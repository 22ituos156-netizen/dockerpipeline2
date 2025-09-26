pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/22ituos156-netizen/dockerpipeline2']])
      }
    }

    stage('Build Image') {
      steps {
        script {
          if (isUnix()) {
            sh 'docker build -t krishg112/dockerpipeline .'
          } else {
            bat 'docker build -t krishg112/dockerpipeline .'
          }
        }

      }
    }

    stage('Docker Push') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
          script {
            if (isUnix()) {
              sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
              sh 'docker push krishg112/dockerpipeline'
              sh 'docker logout'
            } else {
              bat 'docker login -u %DOCKERHUB_USERNAME% -p %DOCKERHUB_PASSWORD%'
              bat 'docker push krishg112/dockerpipeline'
              bat 'docker logout'
            }
          }

        }

      }
    }

  }
}