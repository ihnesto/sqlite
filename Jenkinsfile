properties([pipelineTriggers([githubPush()])])

pipeline {
    agent any

  
    
    stages {
        /* stage('Checkout SCM') {
            steps {
                checkout([
                 $class: 'GitSCM',
                 branches: [[name: 'master']],
                 userRemoteConfigs: [[
                    url: 'https://github.com/ihnesto/sqlite.git',
                    credentialsId: '',
                 ]]
                ])
            }
        } */

        stage('Get src') {
            steps {
                // sh 'git clone https://github.com/ihnesto/popa3d.git'
                git 'https://github.com/ihnesto/sqlite.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mkdir -p ../build'
                dir('../build') {
                    sh 'pwd'
                    sh 'ls -al'
                    sh '../sqlite/configure'
                    sh 'make'    
                    sh 'make sqlite3.c'
                    sh 'make quicktest'
                }
            }
        }
        stage('Deploy') {
            steps{
                sshagent(credentials : ['test-deploy']) {
                    sh 'scp ./sqlite3 root@b.simplehub.xyz:/root/'
                }
    }

        }
    }
}
