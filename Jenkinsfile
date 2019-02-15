pipeline {
  agent any
    tools { 
        maven 'my_maven' 
    }
    stages{
      stage ('Build'){
        steps{
	  echo 'Maven Build'
          sh 'mvn -f pom.xml clean deploy'
	    }
          }
      stage('Results') {
          junit '**/target/surefire-reports/TEST-*.xml'
          archive 'target/*.jar'
            }

          }
     }
