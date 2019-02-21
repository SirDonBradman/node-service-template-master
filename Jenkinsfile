@Library('jenkins-pipeline-util') _

def notifySlack(phase, channel = '#matto-scratch') {
  def message = "Build ${phase} - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
  slackSend message: message, channel: channel
}

pipeline {
    agent {
      dockerfile {
        filename 'Dockerfile.build'
        // assume HTTP_PROXY_URL is defined as a jenkins system level env var
        additionalBuildArgs "--build-arg HTTP_PROXY=${env.HTTP_PROXY_URL}"
      }
    }
    stages {
        stage('Install') {
          steps {
            sh 'env'
            script {
              setupStandardNodeBuild(script: this)
            }
          }
        }
        stage('Validate') {
          steps {
            script {
              nodeValidate(script: this)
            }
          }
        }
        stage('Deploy') {
          steps {
            script {
              if (env.BRANCH_NAME == 'master') {
                nodePruneZipDeploy(script: this)
              }
            }
          }
        }
    }
    post {
      success {
        notifySlack('Success')
      }
      failure {
        notifySlack('Failure')
      }
    }
}