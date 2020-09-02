pipeline {
    agent any
    parameters { 
      string( name: 'commitID' ) 
    }
    environment {
        Docker_user_name     = credentials('Docker_user_name')
        Docker_password	     = credentials('Docker_password	')
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
          sh "docker tag node-app $Docker_user_name/node-app"
          sh "docker login -u $Docker_user_name -p $Docker_password"
          sh "docker push $Docker_user_name/node-app"
        }
      }
    }
}