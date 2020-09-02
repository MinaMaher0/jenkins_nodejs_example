pipeline {
    agent any
    parameters { 
      string( name: 'commitID' ) 
    }
    stages {
      stage('print commit id'){
        steps{
          sh "echo "
        }
      }
      stage('Build docker image'){
        steps{
          dir('app') {
              git url: 'https://github.com/dobromir-hristov/todo-app'
              sh "git checkout ${params.commitID}"
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