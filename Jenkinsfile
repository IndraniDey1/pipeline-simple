node {
  stage('build & deploy') {
    openshiftBuild bldCfg: 'pipeline-simple',
      namespace: 'idey-cicd-development',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'pipeline-simple',
      namespace: 'idey-cicd-development'
  }
  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }
  stage('deploy to test') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'idey-cicd-development',
      srcTag: 'latest',
      destinationNamespace: 'testing',
      destStream: 'hellopythonapp',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'idey-cicd-testing'
  }
  stage('approval (production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }
  stage('deploy to production') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'idey-cicd-development',
      srcTag: 'latest',
      destinationNamespace: 'production',
      destStream: 'hellopythonapp',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'idey-cicd-production'
  }
}
