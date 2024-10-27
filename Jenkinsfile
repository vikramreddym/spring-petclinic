pipeline {
    agent {label 'JDK17'}
    tools {
        jdk 'JDK8'
        maven '3.8.4'

    }
    options {
        timeout(time: 1, unit: 'HOURS')
        retry(3)
    }
    triggers {
        cron('0 * * * *')
    }
    stages{
        stage('SourceCode') {
            steps {
                git branch: 'declarative', url: 'https://github.com/vikramreddym/spring-petclinic.git'
            }
        }

        stage('Build the code'){
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archiving artifacts & Junit test results') {
            steps {
                junit testResults: 'target/surefire-reports/*.xml'
            }
        }
    }
    post {
        success {
            echo "Success"
        }
        unsuccessful {
            echo "failure"
        }
    }
}