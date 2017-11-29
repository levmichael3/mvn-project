pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        ws(dir: 'mvn-project') {
          git 'https://github.com/levmichael3/mvn-project.git'
        }
        
      }
    }
    stage('Prepare') {
      steps {
        sh '''mvnHome=$MAVEN_HOME
${mvnHome}/bin/mvn clean validate -Dmaven.test.failure.ignore -Dmaven.clean.failOnError=false -Dmaven.clean.failOnError=false'''
      }
    }
    stage('Build') {
      steps {
        sh '''mvnHome=$MAVEN_HOME
$mvnHome/bin/mvn package -s ${mvnHome}/conf/settings.xml -e -f pom.xml'''
      }
    }
  }
}