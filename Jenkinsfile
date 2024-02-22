pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
        APP_NAME = "Red-app"
        RELEASE = "1.0.0"
        DOCKER_USER = "rajumb8080"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }
        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/Raju8549/register-app.git'
                }
        }
        stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv('Sonar-Server') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Red-app \
                        -Dsonar.projectKey=Red-app'''
                }
            }
        }
        stage("Build Application"){
                steps {
                    sh "mvn clean package"
                }
        }    
       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }
    }
}
