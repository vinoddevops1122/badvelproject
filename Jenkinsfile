pipeline{
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Git checkout'){
            steps{
                git branch: 'main', credentialsId: 'gitcred', url: 'https://github.com/vinoddevops1122/badvelproject.git'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean package'
            }
        }
    }
}
