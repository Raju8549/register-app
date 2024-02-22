pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
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
