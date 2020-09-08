pipeline {
    agent any
    parameters { 
      choice(name: 'environment', choices: ['dev', 'test'], description: 'Pick which envirnment want to deploy')
    }
    environment {
        Nexus_IP = credentials('Nexus_IP')
        mysql_host     = credentials('mysql_host')
        mysql_username     = credentials('mysql_username')
        mysql_password     = credentials('mysql_password')
        mysql_database	     = credentials('mysql_database')
    }
    stages {
      stage('replace secrets and namespace value'){
        steps{
          sh "sed -i 's/namespace-value/${params.environment}/g' *.yaml"
          sh "sed -i 's/nexus-IP/$Nexus_IP/g' app-deployment.yaml"
          sh "sed -i 's/host-value/$mysql_host/g' app-secret.yaml"
          sh "sed -i 's/username-value/$mysql_username/g' app-secret.yaml"
          sh "sed -i 's/password-value/$mysql_password/g' app-secret.yaml"
          sh "sed -i 's/database-value/vodafone-${params.environment}/g' app-secret.yaml"
        }
      }

      stage('deploying the app'){
        steps{
          sh "ansible-playbook playbook.yaml"
        }
      }
    }
}