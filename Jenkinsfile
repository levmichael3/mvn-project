node {
  def mvnHome = "${env.MAVEN_HOME}"
  def pom, version

  stage('Checkout') {
    // Clean any failed build leftovers and checkout
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanBeforeCheckout']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/levmichael3/mvn-project.git']]])
    // pom = readMavenPom file: 'pom.xml'
  }
  stage('Prepare') {
   sh "'${mvnHome}/bin/mvn' clean validate" +
    "-Dmaven.test.failure.ignore -Dmaven.clean.failOnError=false -Dmaven.clean.failOnError=false"
  }
  stage('Build') {
    sh "'${mvnHome}/bin/mvn' package " +
    "-s ${mvnHome}/conf/settings.xml " +
    "-e -f pom.xml"
  }
  stage('SonarQube analysis') {
    withSonarQubeEnv('sonar') {
      sh "'${mvnHome}/bin/mvn' sonar:sonar " +
      "-e -f pom.xml -Dsonar.host.url=http://localhost:9000"
    }
  }
  stage("Quality Gate"){
    timeout(time: 1, unit: 'HOURS') {
      def qg = waitForQualityGate()
      if (qg.status != 'OK') {
        error "Pipeline aborted due to quality gate failure: ${qg.status}"
      }
    }
  }
  stage('Publish') {
    nexusPublisher nexusInstanceId: 'Nexus', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'web/target/time-tracker-web-0.3.1.war']], mavenCoordinate: [artifactId: 'time-tracker-web', groupId: 'maven-group', packaging: 'war', version: '0.3.2']]]
  }
} 
