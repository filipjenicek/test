#!/usr/bin/env groovy

pipeline {
    //agent any
//agent {
//    docker {
//        image 'maven:3-alpine'
//        args  '-v /tmp:/tmp'
//    }
//}
    agent { dockerfile { dir 'docker' } }

    stages {
        stage('Prepare') {
            steps {
                sh 'echo xx'
                sh 'echo xy'
            }
        }
        stage('Build') {
            steps {
                sh 'pwd'
                sh 'ls -al'
            }
        }
        stage('Deploy') {

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
