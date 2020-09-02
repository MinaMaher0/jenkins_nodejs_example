pipeline {
    agent any
    parameters { 
      choice(name: 'environment', choices: ['dev', 'test'], description: 'Pick which envirnment want to deploy')
    }
    environment {
        mysql_host     = credentials('mysql_host')
        mysql_username     = credentials('mysql_username')
        mysql_password     = credentials('mysql_password')
        mysql_database	     = credentials('mysql_database')
    }
    stages {
      stage('replace secrets and namespace value'){
        steps{
          sh 'sed -i "s/namespace-value/${params.environment}/g" *.yaml'
          sh 'sed -i "s/host-value/$mysql_host/g" app-secret.yaml'
          sh 'sed -i "s/username-value/$mysql_username/g" app-secret.yaml'
          sh 'sed -i "s/password-value/$mysql_password/g" app-secret.yaml'
          sh 'sed -i "s/database-value/$mysql_database${params.environment}/g" app-secret.yaml'
        }
      }

      stage('deploying the app'){
        steps{
          sh "kubectl apply -f mysql-service.yaml"
          sh "kubectl apply -f app-secret.yaml"
          sh "kubectl apply -f app-deployment.yaml"
          sh "kubectl apply -f app-service.yaml"
        }
      }
    }
}