#!/usr/bin/env groovy

pipeline {
    agent any  

    stages {
        stage ('Cleanup') {
            steps {
                echo "nic"
                //sh '[ ! -d build_dir ] || sudo /home/jenkins/rm-build_dir.sh'
            }
        }

        stage ('Docker') {
            steps {
                sh '[ -f docker/crosstools-mips-gcc-4.6-linux-3.4-uclibc-0.9.32-binutils-2.21.Rel1.2.tar.bz2 ] || cp /home/ubnt/crosstools-mips-gcc-4.6-linux-3.4-uclibc-0.9.32-binutils-2.21.Rel1.2.tar.bz2 docker/'
                sh 'docker build docker -t onu'
            }
        }

        stage('Build') {
            steps {
                sh 'cat /etc/issue'
                sh 'docker run --rm -t -v "$PWD:/build/:rw" onu /bin/bash -c "cd /build && ls -al"'
                //sh 'docker run --rm -t -v "$PWD:/build/:rw" onu /bin/bash -c "cd /build && ./build.sh"'
            }
        }

        stage('Deploy') {
            steps {
                sh 'pwd'
                sh 'ls -al'
                sh 'ls -al build'
                archiveArtifacts artifacts: 'build_dir/images/SFU*.bin', fingerprint: true
                sh 'scp build_dir/images/SFU*.bin autotest-onu@10.167.167.150:ftp/'
            }
        }

        stage('Tests') {
            steps {
                sh 'cat /etc/issue'
                sh 'touch test.xml'
                sh 'false'
                junit keepLongStdio: true, testResults: 'test.xml'

            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
            junit keepLongStdio: true, testResults: 'test.xml'
        }
        success { 
            echo 'Good'
        }
        failure { 
            echo 'Failure'
        }
    }
}
