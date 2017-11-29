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
    stage('Prepare') {
      steps {
        sh '''def mvnHome = "${env.MAVEN_HOME}"
sh "\'${mvnHome}/bin/mvn\' clean validate" +
    "-Dmaven.test.failure.ignore -Dmaven.clean.failOnError=false -Dmaven.clean.failOnError=false"'''
      }
    }
  }
}