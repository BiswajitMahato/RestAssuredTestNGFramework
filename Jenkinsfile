@Library('zapp-utilities')
import com.zapp.utilities
utils = new utilities()
pipeline {
    agent any/{ label "zapp-dev-env4" }
    parameters{
            string(name: 'settings_id', defaultValue: 'pwba-settings', description: 'settings xml to be used')
    }
    tools { 
        maven 'maven-3.8.6'
        jdk "jdk-11.0.5"
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '4'))
        skipDefaultCheckout(true)
        disableConcurrentBuilds()
    }
    environment{
    
    }
    stages {
        stage('Checkout_Cucumberframework') {
            steps {
                deleteDir()
                sh "mkdir ${component}"
                dir ("${component}"){
                    checkout scm
                }
                script{
                    currentBuild.description = ""
                }
                echo "This is Build stage"
            }
        }
        stage('Build_CucumberFramework') {
            steps {
                dir ("${component}"){
                
                    script {
                    
                        util.mvn("clean install verify serenity:aggregate -DtestEnvironment=src/test/resources/properties/anc.yml -DtestProperties=abc -V", param.setting_id)
                    
                    }
                }
                
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
            //emailext body: 'This is auto-generated mail from Jenkins ', subject: 'Jenkins mail test', to: 'biswajitmahato1994@gmail.com'
            publishHTML target:[
                allowMissing: false,
                alwaysLinkToLastBuilt: true,
                KeepAll: true,
                reportDir: 'project/target/site/serenity/',
                reportFiles: 'index.html'
                reportName: 'Serenity Report'
            
            ]
            
            emailext body: "<b>This is auto-generated mail from Jenkins</b><br>Project: ${env.JOB_NAME} <br>Build Number: {env.BUILD_NUMBER}",
                     mimeType: "text/html",
                     attachmentsPattern: "**/serenity-summary.html",
                     subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Project Cucumber Automation Report",
                     to: "abc@gmail; xyz@abc.com"
    }
}
