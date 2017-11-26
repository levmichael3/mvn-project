pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        ws(dir: 'mvn-project') {
          build 'Automat-IT'
        }
        
      }
    }
  }
}