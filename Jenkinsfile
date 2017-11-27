pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        ws(dir: 'mvn-project') {
          git 'https://github.com/levmichael3/mvn-project.git'
        }
        
      }
    }
  }
}