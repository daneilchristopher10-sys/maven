pipeline {
    agent any
    
    tools {
        maven 'maven-3'
        jdk 'jdk-26'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Clean & Compile') {
            steps {
                bat 'mvn clean compile'
            }
        }
        
        stage('Run Tests') {
            steps {
                bat 'mvn test'
            }
        }
        
        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }
    }
    
    post {
        success {
            echo '✅ CI Pipeline Successful!'
        }
        failure {
            echo '❌ CI Pipeline Failed!'
        }
    }
}