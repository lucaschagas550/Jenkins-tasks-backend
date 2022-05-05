pipeline{
    agent any
    stages{
        stage('Build Backend'){
            steps{
                bat 'mvn clean package -DskipTests=true'
            }   
        }
        stage('Unit Tests'){
            steps{
                bat 'mvn test'
            }   
        }
        stage('Deploy BackEnd'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'TomCat_Login', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'            }   
        }
        stage('API Test'){
            steps{
                dir('') {
                    git credentialsId: 'GitHub_Login', url: 'https://github.com/lucaschagas550/Jenkins-tasks-test'
                    bat 'mvn test'
                }
            }
        }        
    }
}