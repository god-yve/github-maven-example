pipeline {
  agent any
  stages {
    stage('Build & Test') {
      agent {
        node {
          label 'docker-1'
        }

      }
      steps {
        sh 'mvn clean package'
        stash(name: 'build-test-artifacts', includes: '**/target/surefire-reports/TEST-*.xml, **/target/*.jar')
      }
    }
    stage('Report & Publish') {
      agent {
        node {
          label 'docker-1'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit 'target/surefire-reports/TEST-*.xml'
        archiveArtifacts(artifacts: '**/target/*.jar', onlyIfSuccessful: true)
      }
    }
  }
}