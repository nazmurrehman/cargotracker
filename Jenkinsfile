pipeline {
  agent any
    tools { 
        maven 'my_maven' 
    }
    stages{
      stage('Build') {
      agent {
        docker {
          /*
           * Reuse the workspace on the agent defined at top-level of Pipeline but run inside a container.
           * In this case we are running a container with maven so we don't have to install specific versions
           * of maven directly on the agent
           */
          reuseNode true
          image 'maven:3.5.0-jdk-8'
        }
      }
      steps {
        // using the Pipeline Maven plugin we can set maven configuration settings, publish test results, and annotate the Jenkins console
        withMaven(options: [findbugsPublisher(), junitPublisher(ignoreAttachments: false)]) {
          sh 'mvn clean findbugs:findbugs package'
        }
      }
      post {
        success {
          // we only worry about archiving the jar file if the build steps are successful
          archiveArtifacts(artifacts: '**/target/*.war', allowEmptyArchive: true)
        }
      }
    }

      stage('archive') {
         steps {
             sh 'curl -v -u admin:admin123 --upload-file web/target/*.war http://localhost:8081/nexus/content/repositories/my_repo'
               }
           }
    }
}
