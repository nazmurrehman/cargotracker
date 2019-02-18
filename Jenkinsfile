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
                   sh 'curl -v -u admin:admin123 --upload-file /var/jenkins_home/workspace/test_pipeline/target/*.war http://10.0.1.115:8081/nexus/content/repositories/my_repo'
                    }
                }
     
        }
}
