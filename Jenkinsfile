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
                sh 'pwd'
                sh 'ls -al'
            }
        }

        stage('Prepare') {
            agent { dockerfile { dir 'docker' } }
            steps {
                sh 'echo xx'
                sh 'echo xy'
            }
        }
        stage('Build') {
            agent { dockerfile { dir 'docker' } }
            steps {
                sh 'pwd'
                sh 'ls -al'
                sh 'ls -al /tmp'
            }
        }
        stage('Deploy') {
            agent { dockerfile { dir 'docker' } }
            steps {
                sh 'echo dep'
            }
        }
        stage('Tests') {
agent any
            steps {
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
