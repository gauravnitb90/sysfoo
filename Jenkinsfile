pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Compiling Sysfoo'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Test Sysfoo'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      when {
              beforeAgent true
              branch 'master'
            }
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Package Sysfoo'
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.war'
      }
    }

    stage('Docker BP') {
      when {
              beforeAgent true
              branch 'master'
            }
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("gauravnitb/sysfoo:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
            dockerImage.push("dev")
          }
        }

      }
    }
    stage('Deploy to Dev') {
      when {
             beforeAgent true
             branch  'master'
           }
      agent any
      steps {
        echo 'Deploying to Dev Environment with Docker Compose'
        sh 'docker-compose up -d'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}