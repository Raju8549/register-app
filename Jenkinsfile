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
         stage('SonarQube Analysis') {
            def mvn = tool 'maven3';
                withSonarQubeEnv() {
                  sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Red-app -Dsonar.projectName='Red-app'"
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
