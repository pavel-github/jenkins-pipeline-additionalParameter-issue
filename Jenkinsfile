def dockerTag = ""

pipeline {
  agent { label 'nodejs' }

  stages {
    stage('Checkout') {
        steps {
            deleteDir()
            git 'https://github.com/pavel-github/jenkins-pipeline-additionalParameter-issue'
        }
    }
    
    stage('Security') {
        steps {
            sh 'echo 0.11.1 > VERSION'
            dockerTag = sh(returnStdout: true, script: 'cat VERSION')

            //withEnv(["VERSION=\$(cat VERSION)"]){
                snykSecurity monitorProjectOnBuild: false,
                             snykInstallation: 'snyk@latest',
                             snykTokenId: 'my-snyk-api-token',
                             failOnIssues: true,
                             additionalArguments: "--docker ${dockerTag}"
                sh 'echo $VERSION'
            //}
        }
    }
  }
}
