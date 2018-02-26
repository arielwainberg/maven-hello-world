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
        stage('Step-2: Compiling And Creating The Job') {
            steps{
                dir ('my-app') {
                    sh "mvn package"
                }
            }
        }
        stage('Step-3: Executing the jar file') {
            steps{
                dir ('my-app') {
                    sh "java -jar target/my-app-1.0-SNAPSHOT.jar"
                }
            }
        }
    }
    
    
}