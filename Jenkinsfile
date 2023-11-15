pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }
    stages {
        stage('Git Checkout') {
            steps {
              git 'https://github.com/learnmk/BoardgameListingWebApp.git'
            }
        }
        stage('maven compile') {
            steps {
              sh 'mvn compile'
            }
        }
        stage('maven test') {
            steps {
              sh 'mvn test'
            }
        }
        stage('sonar scanner') {
            steps {
              withSonarQubeEnv('sonar') {
            sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=BoardgameList \
            -Dsonar.projectKey=BoardgameList -Dsonar.java.binaries=. '''
              }
            }
        }
         stage('Quality gate') {
            steps {
              waitForQualityGate abortPipeline: false
            }
        }
    }
}
