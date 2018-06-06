pipeline {
    agent none
    stages {
        stage ('Checkout') {
          steps {
            git 'https://github.com/ashishrpandey/jenkinspipeline.git'
          }
        }
        stage('Build') {
            agent { docker 'maven:3.5-alpine' }
            steps {
                sh 'mvn clean package'
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Deploy') {
          steps {
            input 'Do you approve the deployment?'
            sh 'cp -r target/*.jar /opt/pet/'
            sh 'nohup java -jar /opt/pet/spring-petclinic-1.5.1.jar &'
          }
        }
    }
}
