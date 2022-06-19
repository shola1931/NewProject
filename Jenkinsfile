pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
              git branch: 'main', url: 'https://github.com/shola1931/NewProject.git'
            }
        }
        stage('SonarQube analysis'){
            steps{
                withSonarQubeEnv('sonar'){
                    sh 'mvn -f SampleWebApp/pom.xml clean package sonar:sonar'
                }
            }
        }


        stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        }
         stage('Build with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn package'
            }
        }
         stage('Deploy to Somewhere') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '15edea7f-6b57-434a-b2c7-ebc284416277', 
                path: '', 
                url: 'http://52.87.180.70:8080/')], 
                contextPath: 'default', 
                war: '**/*.war'
            }
        }
    }
}
