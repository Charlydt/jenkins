pipeline {
  agent any
  tools {
    mvn 'maven-3.8'
  }
  stages {
    stage("build jar") {
      steps {
        script {
          echo "building the application..."
          sh 'mvn package'
        }
      }
    }
    stage("build image") {
        steps {
        script {
            echo "building the docker image..."
            withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]){
            sh 'docker build -t charlydt/jenkins-app:1.0 .'
            sh "echo $PASS | docker login -u $USER --password-stdin"
            sh 'docker push charlydt/jenkins-app:1.0'
            }
        }
        }   
    }
    stage("deploy") {
        steps {
        script {
            echo "deploying the application..."
        }
        }
    }
  }
}
