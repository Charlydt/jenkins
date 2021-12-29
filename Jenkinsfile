@Library('jenkins-shared-library')
def gv

pipeline {
  agent any
  tools {
    maven 'maven-3.8'
  }
  stages {
    stage("init") {
      steps {
        script {
          gv = load "script.groovy"
        }
      }
    }
    stage("test") {
      steps {
        script {
          echo "Testing the application 123..."
          echo "Executing pipeline for branch $BRANCH_NAME"
        }
      }
    }
    stage("build jar") {
      when {
        expression {
          BRANCH_NAME == 'main'
        }
      }
      steps {
        script {
          buildJar()
        }
      }
    }
    stage("build and push image") {
      when {
        expression {
          BRANCH_NAME == 'main'
        }
      }      
      steps {
          script {
            buildImage 'charlydt/jenkins-app:1.1'
            dockerLogin()
            dockerPush 'charlydt/jenkins-app:1.1'
          }
      }   
    }
    stage("deploy") {
      when {
        expression {
          BRANCH_NAME == 'main'
        }
      }      
      steps {
          script {
              gv.deployApp()
          }
      }
    }
  }
}
