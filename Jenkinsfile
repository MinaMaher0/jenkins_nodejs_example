pipeline {
    agent any
    parameters { 
      string( name: 'commitID' ) 
    }
    stages {
      stage('Build docker image'){
        steps{
          dir('app') {
              git url: 'https://github.com/MinaMaher0/jenkins_nodejs_example'
              sh "git checkout ${params.commitID}"
              sh "ls"
              sh "cat nodeapp/app.js"
             // sh 'docker build -t node-app .'
          }
        }
      }
      // stage('pushing the image to docker hub'){
      //   steps{
      //     sh 'docker '
      //   }
      // }
    }
}