pipeline {
    agent any
    parameters { 
      string( name: 'commitID' ) 
    }
    environment {
        Docker-user-name     = credentials('Docker-user-name')
        Docker-password	     = credentials('Docker-password	')
    }
    stages {
      stage('Build docker image'){
        steps{
          dir('app') {
              git url: 'https://github.com/MinaMaher0/jenkins_nodejs_example'
              sh "git checkout ${params.commitID}"
              sh 'docker build -t node-app .'
          }
        }
      }

      stage('pushing the image to docker hub'){
        steps{
          sh "docker tag node-app $Docker-user-name/node-app"
          sh "docker login -u $Docker-user-name -p $Docker-password"
          sh "docker push $Docker-user-name/node-app"
        }
      }
    }
}