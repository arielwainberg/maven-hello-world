pipeline {
    agent any
    parameters {
        string(name: 'username', defaultValue: 'jenkins', description: 'Username to use for scp')
        string(name: 'dev_env', defaultValue: '10.12.100.145', description: 'Developers Server')
        string(name: 'prd_env', defaultValue: '10.12.100.146', description: 'Production Server')
        string(name: 'EmailAdress', defaultValue: 'arielw@pcb.co.il', description: 'Notifications Email Address')
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
            stage ('step-4: Deployments'){
               parallel{
                    stage ('Deploy to Staging'){
                        steps {
                            dir ('my-app') {
                                sh "scp -i /var/lib/jenkins/jenkins.pem ./target/*.jar ${params.username}@${params.dev_env}:/home/jenkins/helloworld_maven"
                            }
                        }
                    }
                    stage ("Deploy to Production"){
                        steps {
                            dir ('my-app') {
                                sh "scp -i /var/lib/jenkins/jenkins.pem ./target/*.jar ${params.username}@${params.prd_env}:/home/jenkins/helloworld_maven"
                            }
                        }
                    }
                }
            }
        }
        post {
            success {
                mail (to: "${params.EmailAdress}", subject: "Job '${env.JOB_NAME}' Build(#${env.BUILD_NUMBER}) Succeded" , body: "Job:'${env.JOB_NAME}' on Build:(#${env.BUILD_NUMBER}) Succesesfully ran.")
            }
            failure {
                mail (to: "${params.EmailAdress}", subject: "Job '${env.JOB_NAME}' Build(#${env.BUILD_NUMBER}) Failed" , body: " Job:'${env.JOB_NAME}' on Build:(#${env.BUILD_NUMBER}) Failed To run, go back to Debug!")
            }
        }
    }