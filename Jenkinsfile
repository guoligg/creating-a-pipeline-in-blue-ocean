pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '''-p 3000:3000
-v /root/node_modules:/root/.jenkins/workspace/_a-pipeline-in-blue-ocean_master/node_modules'''
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
}