pipeline {
  agent any
  stages {
    stage('ApplyChanges') {
      steps {
        snApplyChanges()
      }
    }

    stage('AppPublish') {
      steps {
        snPublishApp(obtainVersionAutomatically: true)
      }
    }

    stage('AppInstall') {
      steps {
        snInstallApp()
      }
    }

    stage('RunTest') {
      steps {
        snRunTestSuite()
      }
    }

  }
}