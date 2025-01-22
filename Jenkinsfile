pipeline {
    agent any
    
    tools{
        maven "Maven-3.9.9"
    }    

    stages {
        stage('Git Clone') {
            steps {
               git branch: 'main', url: 'https://github.com/shubham-0211/01_products_api_Backend.git'
            }
        }
        stage('Maven Build'){
            steps{
             sh 'mvn clean package'
            }
        }
        stage('Docker Image'){
            steps{
             sh 'docker build -t shubhamghongade/products_api .'
            }
        }
        stage('Docker Image push'){
            steps{
            withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {
                   sh 'docker login -u shubhamghongade -p ${docker_pwd}'
                   sh 'docker push shubhamghongade/products_api'
            }
            }
        }
        stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }        
    }
}
