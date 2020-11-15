properties([pipelineTriggers([githubPush()])])

pipeline {
    agent any

    /* triggers {
        pollSCM('* * * * *')
    } */
    
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout([
                 $class: 'GitSCM',
                 branches: [[name: 'master']],
                 userRemoteConfigs: [[
                    url: 'https://github.com/ihnesto/popa3d.git',
                    credentialsId: '',
                 ]]
                ])
            }
        }

        stage('Get src') {
            steps {
                // sh 'git clone https://github.com/ihnesto/popa3d.git'
                git 'https://github.com/ihnesto/popa3d.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'make'
            }
        }
        stage('Deploy') {
            steps{
                sshagent(credentials : ['test-deploy']) {
                    sh 'scp ./popa3d root@b.simplehub.xyz:/root/'
                }
    }

        }
    }
}
