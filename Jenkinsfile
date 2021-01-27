pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'Compiling Sysfoo'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'Test Sysfoo'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'Package Sysfoo'
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}