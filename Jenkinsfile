pipeline{
    agent any
    environment {     
    DOCKERHUB_CREDENTIALS= credentials('docker-hub-credential') 
}
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vprasadreddy/java-springboot.git']])
                sh 'mvn clean install'
            }
        }
        stage('build docker image'){
            steps{
            sh 'docker build -t prasadreddy2349/devops-integration:latest .'
        }
        }
        stage('Push docker image'){
            steps{
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    echo 'Login successful'
                    sh 'docker push prasadreddy2349/devops-integration:latest'
        }
    }
}
  post{
    always {  
      sh 'docker logout'           
    }      
  } 
}