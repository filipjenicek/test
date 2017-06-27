#!/usr/bin/groovy
pipeline {
    //agent any
agent {
    docker {
        image 'maven:3-alpine'
        label 'my-defined-label'
        args  '-v /tmp:/tmp'
    }
}
    stages {
        stage('Prepare') {
            steps {
                sh 'echo xx'
                sh 'echo xy'
            }
        }
        stage('Build') {
            steps {
                sh '/home/jenkins/build/gpon-onu.sh'
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
