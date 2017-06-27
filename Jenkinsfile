#!/usr/bin/env groovy

stage('Build') {
    node {
        echo 'Cleanup'
        //sh '[ ! -d build_dir ] || sudo /home/jenkins/rm-build_dir.sh'
        
        echo 'Checkout'
        checkout scm
        
        echo 'Prepare docker'
        sh '[ -f docker/crosstools-mips-gcc-4.6-linux-3.4-uclibc-0.9.32-binutils-2.21.Rel1.2.tar.bz2 ] || cp /home/ubnt/crosstools-mips-gcc-4.6-linux-3.4-uclibc-0.9.32-binutils-2.21.Rel1.2.tar.bz2 docker/'
        sh 'docker build docker -t onu'

        echo 'Build'
        sh 'cat /etc/issue'
        sh 'docker run --rm -t -v "$PWD:/build/:rw" onu /bin/bash -c "cd /build && ls -al"'
        //sh 'docker run --rm -t -v "$PWD:/build/:rw" onu /bin/bash -c "cd /build && ./build.sh"'

        echo 'Deploy'
        sh 'ls -al'
        sh 'ls -al build'
        archiveArtifacts artifacts: 'build_dir/images/SFU*.bin', fingerprint: true
        stash includes: 'build_dir/images/SFU*.bin', name: 'firmware' 
    }
}

stage('Test') {
    parallel test_fh: {
        node('test_fh') {
            unstash 'firmware'
            sh 'touch test.xml'
            lock('gpon-test-fh') {
                sh 'ls -al'
                junit keepLongStdio: true, testResults: 'test.xml'
            }
        }
    },
    test_hw: {
        node('test-hw') {
            unstash 'firmware'
            lock('gpon-test-fh') {
                sh 'ls -al'
            }
        }
    }
}
