pipeline {
    agent any
    tools {nodejs "nodejs"}

    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {

                sh './jenkins/scripts/test.sh'
                sshPublisher(publishers: [sshPublisherDesc(configName: 'UL-Client Ec2 1', sshRetry: [retries: 2, retryDelay: 10000], transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'demo', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '/Users/vivek/.jenkins/workspace/simple-node-js-react-npm-app/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
