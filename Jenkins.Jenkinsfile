pipeline {

    agent any
    parameters {
        string(name: 'EmailAdress', defaultValue: 'ariel@xxxxx.co.il', description: 'Notification Email Address')
    }
    stages {
        stage('Step-1: Clean Mave ') {
            steps {
                sh "cd my-app"
                sh "mvn clean"
            }
        }
        stage ('Step-2: Step-2') {
            steps{
                sh "echo hello"
            }
        }
    }
    
    
}