pipeline {
  agent any
  environment {
    APPSYSID = '00f35c601b2b9410fe0165f8bc4bcb06'
    CREDENTIALS = '18be2029-2e62-4070-8828-dbb3aa39f0f0'
    DEVENV = 'https://chiarngdevdemo.service-now.com/'
    TESTENV = 'https://chiarngtestdemo.service-now.com/'
    PRODENV = 'https://chiarngproddemo.service-now.com/'
    TESTSUITEID = 'b1ae55eedb541410874fccd8139619fb'
    BUILDTVERSION = '1.0.2'
    NEXTDOTVERSION = '1.0.3'
    NEXTMINORVERSION = '1.1.0'
  }
  stages {
    stage('Build') {
      steps {
        snApplyChanges(appSysId: ${APPSYSID}, branchName: 'somefeature', url: ${DEVENV}, credentialsId: ${CREDENTIALS})
        snPublishApp(credentialsId: ${CREDENTIALS}, appSysId: ${APPSYSID}, obtainVersionAutomatically: true, url: ${DEVENV})
      }
    }

    stage('Test') {
      steps {
        snInstallApp(credentialsId: ${CREDENTIALS}, url: ${TESTENV}, appSysId: ${APPSYSID})
        snRunTestSuite(credentialsId: ${CREDENTIALS}, url: ${TESTENV}, testSuiteSysId: ${TESTSUITEID}, withResults: true)
      }
    }

    stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: '18be2029-2e62-4070-8828-dbb3aa39f0f0', url: ${PRODENV}, appSysId: ${APPSYSID})
      }
    }

  }
}
