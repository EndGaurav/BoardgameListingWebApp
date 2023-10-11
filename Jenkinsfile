pipeline {
    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('Git Checkout') {
            steps {
               git 'https://github.com/EndGaurav/BoardgameListingWebApp.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Sonarqube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh ''' ${SCANNER_HOME}/bin/sonar-scanner \
                    -Dsonar.projectName=thisBoard \
                    -Dsonar.projectKey=thisBoard  -Dsonar.java.binaries=.'''
                }
            }
        }
    }
}

