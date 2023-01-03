pipeline {
    agent any
    tools { 
        maven 'maven-3.8.6' 
    }
    stages {
        stage('Build') {
            steps {
                echo "This is Build stage"
            }
        }
        stage('Test) {
            steps {
                echo "This is Test stage"
            }
        }
        stage('Deploy') {
            steps {
                echo "This is Deploy stage"
            }
        }
 
    }
   post {
        always {
            emailext body: 'This is auto-generated mail from Jenkins ', recipientProviders: [contributor()], subject: 'Jenkins mail test', to: 'biswajitmahato1994@gmail.com'
        }
    }
}
