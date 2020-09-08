pipeline {
    agent any
    parameters { 
      string( name: 'commitID' ) 
    }
    environment {
        Nexus_IP = credentials('Nexus_IP')
        Nexus_user_name     = credentials('Nexus_user_name')
        Nexus_password	     = credentials('Nexus_password	')
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
          sh "docker tag node-app $Nexus_IP/node-app"
          sh "docker login -u $Nexus_user_name -p $Nexus_password $Nexus_IP"
          sh "docker push $Nexus_IP/node-app"
        }
      }
    }
}