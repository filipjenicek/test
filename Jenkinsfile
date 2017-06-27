#!/usr/bin/env groovy

pipeline {
    agent any  

    stages {
        stage ('Cleanup') {
            sh '[ -d build_dir ] && sudo /home/jenkins/rm-build_dir.sh'
        }

        stage ('Docker') {
            steps {
                sh '[ -f docker/crosstools-mips-gcc-4.6-linux-3.4-uclibc-0.9.32-binutils-2.21.Rel1.2.tar.bz2 ] || cp /home/ubnt/crosstools-mips-gcc-4.6-linux-3.4-uclibc-0.9.32-binutils-2.21.Rel1.2.tar.bz2 docker/'
                sh 'docker build . -t onu'
            }
        }

        stage('Build') {
            steps {
                sh 'cat /etc/issue'
                sh 'docker run --rm -t -v "$PWD:/build/:rw" onu /bin/bash -c "ls"'
                //sh 'docker run --rm -t -v "$PWD:/build/:rw" onu /bin/bash -c "cd /build && ./build.sh"'
            }
        }

        stage('Deploy') {
            steps {
                echo "Nothing here yet"
            }
        }

        stage('Tests') {
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
