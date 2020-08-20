pipeline {
    agent any
    stages {

       stage('Deploy Infraestructure') {

           when { anyOf {
               branch 'jenkins' 
           }}       

             steps {
                echo 'Deploy the infraestructure'
                sh "./infraestructure/create.sh Able-Infra infraestructure/able-infra.yml infraestructure/able-infra-param.json"
                sh "sleep 240"
                echo 'Deployment of infraestructure complete'
            }
        }


       stage('Deploy Network') {

           when { anyOf {
               branch 'jenkins' 
           }}       

             steps {
                echo 'Deploy Servers'
                sh "./infraestructure/create.sh Able-servers infraestructure/able-servers.yml infraestructure/able-servers-param.json"
                sh "sleep 240"
                echo 'Deployment of servers complete'
            }
        }

       stage('Deploy Jump Server') {

           when { anyOf {
               branch 'jump' 
           }}       

             steps {
                echo 'Deploy Jump Server'
                sh "./jumpserver/create.sh Able-jumpserv jumpserver/able-jump.yml jumpserver/able-jump-param.json"
                sh "sleep 240"
                echo 'Deployment of jump server complete'
            }
        }
    }
}