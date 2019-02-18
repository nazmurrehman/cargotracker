pipeline {
  agent any
    tools { 
        maven 'my_maven' 
    }
    stages{
        stage ('Build'){
         steps{
	  echo 'Maven Build'
          sh 'mvn -f pom.xml clean install'
	    }
          }
        stage ('SonarQube'){
          steps{
              sh 'mvn sonar:sonar -Dsonar.host.url=http://127.0.0.1:9000/sonar'
              }
            }
      stage('archive') {
         steps {
             sh 'curl -v -u admin:admin123 --upload-file web/target/*.war http://localhost:8081/nexus/content/repositories/my_repo'
               }
             }
      }
}
