pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        snApplyChanges(appSysId: '00f35c601b2b9410fe0165f8bc4bcb06', branchName: 'somefeature', url: 'https://chiarngdevdemo.service-now.com/', credentialsId: '18be2029-2e62-4070-8828-dbb3aa39f0f0')
        snPublishApp(credentialsId: '18be2029-2e62-4070-8828-dbb3aa39f0f0', appSysId: '00f35c601b2b9410fe0165f8bc4bcb06', obtainVersionAutomatically: true, url: 'https://chiarngdevdemo.service-now.com/')
      }
    }

    stage('Test') {
      steps {
        snInstallApp(credentialsId: '18be2029-2e62-4070-8828-dbb3aa39f0f0', url: 'https://chiarngtestdemo.service-now.com/', appSysId: '00f35c601b2b9410fe0165f8bc4bcb06')
        snRunTestSuite(credentialsId: '18be2029-2e62-4070-8828-dbb3aa39f0f0', url: 'https://chiarngtestdemo.service-now.com/', testSuiteSysId: 'b1ae55eedb541410874fccd8139619fb', withResults: true)
        snRollbackApp(credentialsId: '18be2029-2e62-4070-8828-dbb3aa39f0f0', url: 'https://chiarngtestdemo.service-now.com/', appSysId: '00f35c601b2b9410fe0165f8bc4bcb06')
      }
    }

    stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(url: 'https://chiarngproddemo.service-now.com/')
      }
    }

  }
}