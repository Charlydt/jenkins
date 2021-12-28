def gv

pipeline {
  agent any
  tools {
    maven 'maven-3.8'
  }
  stages {
    stage("init") {
      script {
        gv = load "script.goovy"
      }
    }
    stage("build jar") {
      steps {
        script {
          gv.buildJar()
        }
      }
    }
    stage("build image") {
        steps {
          script {
            gv.buildImage()
          }
        }   
    }
    stage("deploy") {
        steps {
          script {
              gv.deployApp()
          }
        }
    }
  }
}
