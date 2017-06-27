#!/usr/bin/env groovy

pipeline {
    agent none

    //agent any
//    agent {
//        docker {
//            image 'onu'
//            args  '-v /tmp:/tmp'
 //       }
//    }
    

    stages {
        stage ('Prepare agent') {
            agent any
            steps {
                sh 'cat /etc/issue'
            }
        }

        stage('Prepare') {
            agent { dockerfile { dir 'docker' } }
            steps {
                sh 'cat /etc/issue'
            }
        }
        stage('Build') {
            agent any
            steps {
                sh 'cat /etc/issue'
            }
        }
        stage('Deploy') {
            agent { dockerfile { dir 'docker' } }
            steps {
                sh 'cat /etc/issue'
            }
        }
        stage('Tests') {
            agent any
            steps {
                sh 'cat /etc/issue'
                sh 'touch test.xml'
                junit keepLongStdio: true, testResults: 'test.xml'
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        success { 
            echo 'Good'
        }
        failure { 
            echo 'Failure'
        }


    }

}
