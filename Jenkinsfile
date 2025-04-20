pipeline {
    agent any

    tools {
        maven 'maven3'
        jdk 'jdk17'
    }

    stages {
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test with Coverage') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Static Code Analysis (SonarQube)') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                sh '''
                    trivy fs --scanners config,secret,vuln . || true
                '''
            }
        }

        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
