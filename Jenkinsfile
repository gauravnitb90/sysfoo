pipeline {

  agent any

  tools{
    maven 'Maven 3.6.3' 
  }

  stages {
  	stage('build'){
  		steps{
  			echo 'Compiling Sysfoo'
  			sh 'mvn compile'
  		}
  	}

  	stage('test'){
  		steps{
  			echo 'Test Sysfoo'
  			sh 'mvn clean test'
  		}
  	}

  	stage('package'){
  		steps{
  			echo 'Package Sysfoo'
  			sh 'mvn package -DskipTests'
  		}
  	}
  
  }

}