pipeline {
  agent {
    label 'AWS_Jenkins-slave'
  }

  libraries {
    lib 'jenkins-ci-tad'
  }

  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
    timeout(time: 10, unit: 'MINUTES')
    ansiColor('xterm')
  }

  tools {
    nodejs 'Node16.4.0'
  }

  environment {
    GH_TOKEN = credentials('GithubPAT')
    GIT_CREDENTIALS = credentials('github_semantic_release')
    NPM_TOKEN = credentials('npm-nexus-token')
  }

  stages {
    stage('snyk') {
      steps {
        echo 'Testing Snyk'
        snykSecurity(
          snykInstallation: 'snyk',
          snykTokenId: 'snyk-api',
          organisation : 'pamg-it-operations'
        )
      }
    }
  }

  post {
    cleanup {
      cleanWs()
    }
  }
}