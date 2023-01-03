pipeline {
    agent any
    tools { 
        maven 'maven-3.8.6' 
    }
    stages {
        stage('Checkout git') {
            steps {
               git branch: 'main', url: 'https://github.com/BiswajitMahato/RestAssuredTestNGFramework.git'
            }
        }
        
        stage ('Build & JUnit Test') {
            steps {
                sh 'mvn install' 
            }
            post {
               success {
                    junit 'target/surefire-reports/**/*.xml'
                }   
            }
        }
    }
   post {
        always {
            emailext body: 'This is auto-generated mail from Jenkins ', recipientProviders: [contributor()], subject: 'Jenkins mail test', to: 'biswajitmahato1994@gmail.com'
        }
    }
}
