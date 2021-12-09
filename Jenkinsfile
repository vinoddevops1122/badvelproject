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
        stage('nexus artifactory'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'badvelproject', classifier: '', file: 'target/badvelproject.war', type: 'war']], 
                credentialsId: 'nexus_cred', 
                groupId: 'in.badvel', 
                nexusUrl: '172.31.1.76:8081/', 
                nexusVersion: 'nexus3', protocol: 'http', 
                repository: 'badvelproject-snapshots', 
                version: '1.0-SNAPSHOT'
            }
        }
		stage('deploy to war'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'tomcat_cred', path: '', url: 'http://172.31.34.67:8080/')], contextPath: null, war: 'target/badvelproject.war'
            }
        }
    }
}
