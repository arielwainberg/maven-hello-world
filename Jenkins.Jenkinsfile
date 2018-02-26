pipeline {

    agent any
    parameters {
        string(name: 'EmailAdress', defaultValue: 'ariel@xxxxx.co.il', description: 'Notification Email Address')
    }
    stages {
        stage('Step-1: Clean Mave ') {
            steps {
                dir ('my-app') {
                    sh "mvn clean"
                }
            }
        }
        stage('Step-2: Compileing and creating targetting directory includes the Jar File') {
            steps{
                dir ('my-app') {
                    sh "mvn package"
                }
            }
        }
    }
    
    
}