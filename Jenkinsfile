pipeline{
    agent any
    tools {
        maven 'Maven'
    }
    stages{
        stage('git checkout'){
            steps{
                git credentialsId:'Guiza4',url:'https://github.com/Guiza4/TP5Jenkins.git'
            }  
        }
        
        stage('Build Application'){
            steps{
                sh 'mvn clean install'
            }
        }
        
        stage('Unit Test Execution'){
            steps{
                sh 'mvn test'
            }
        }
        
        stage('Build the Docker Image'){
            steps{
                sh 'docker build -t guiza4/triang7:1.0.0 .'
            }
        }
        
        stage('Upload the Docker Image'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPass')]) {
                sh "echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin"
                sh 'docker push guiza4/triang7:1.0.0'
                }
            }
        }
    }
}
