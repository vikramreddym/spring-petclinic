pipeline {
    agent {label 'JDK17'}
    tools {
        jdk 'JDK17'
        maven '3.8.4'

    }
    options {
        timeout(time: 1, unit: 'HOURS')
        retry(3)
    }
    // triggers {
    //     cron('0 * * * *')
    // }
    parameters {
        choice(name: 'GOAL', choices:['clean', 'clean package', 'clean install'], description: 'Goals for maven')
    }
    stages{
        stage('SourceCode') {
            steps {
                git branch: 'declarative', url: 'https://github.com/vikramreddym/spring-petclinic.git'
            }
        }

        stage('Build the code'){
            steps {
                sh 'mvn ${params.GOAL}'
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