#!/usr/bin/env groovy

pipeline {
    //agent any
agent {
    docker {
        image 'onu'
        args  '-v /tmp:/tmp'
    }
}
//    agent { dockerfile { dir 'docker' } }

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
                sh 'ls -al /tmp'
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo dep'
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
