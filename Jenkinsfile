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
        
      stage('archive') {
         steps {
             sh ' cd /var/lib/docker/volumes/ubuntu_jenkins_data/_data/workspace/test_pipeline/'
             sh 'curl -v -u admin:admin123 --upload-file target/*.war http://18.212.167.103:8081/nexus/content/repositories/my_repo'
               }
             }
      }
}
