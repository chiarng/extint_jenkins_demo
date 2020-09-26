pipeline {
  agent any
  environment {
    APPSYSID = '00f35c601b2b9410fe0165f8bc4bcb06'
    BRANCH = env.BRANCH_NAME
    CREDENTIALS = '18be2029-2e62-4070-8828-dbb3aa39f0f0'
    DEVENV = 'https://chiarngdevdemo.service-now.com/'
    TESTENV = 'https://chiarngtestdemo.service-now.com/'
    PRODENV = 'https://chiarngproddemo.service-now.com/'
    TESTSUITEID = 'b1ae55eedb541410874fccd8139619fb'
    MAJORVERSION = '1'
    MINORVERSION = '0'
    DOTVERSION = '3'
  }
  stages {
    stage('Build') {
      steps {
        snApplyChanges(appSysId: '${APPSYSID}', branchName: '${BRANCH}', 'url: ${DEVENV}', credentialsId: '${CREDENTIALS}')
        snPublishApp(credentialsId: '${CREDENTIALS}', appSysId: '${APPSYSID}', obtainVersionAutomatically: false, url: '${DEVENV}')
      }
    }
    stage('Test') {
      steps {
        snInstallApp(credentialsId: '${CREDENTIALS}', url: '${TESTENV}', appSysId: '${APPSYSID}')
        snRunTestSuite(credentialsId: '${CREDENTIALS}', url: '${TESTENV}', testSuiteSysId: '${TESTSUITEID}', withResults: true)
      }
    }
    stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: '${CREDENTIALS}', url: '${PRODENV}', appSysId: '${APPSYSID}')
      }
    }
  }
}
