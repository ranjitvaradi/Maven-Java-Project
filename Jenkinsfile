def ansible = [:]
         ansible.name = 'ansible'
         ansible.host = '172.31.30.154'
         ansible.user = 'centos'
         ansible.password = 'Rnstech@123'
         ansible.allowAnyHosts = true
def kops = [:]
         kops.name = 'kops'
         kops.host = '172.31.34.51'
         kops.user = 'centos'
         kops.password = 'Rnstech@123'
         kops.allowAnyHosts = true
pipeline {
    agent any

    stages {
                   
	stage('SonarQube analysis') {
         
          steps{
                echo "Sonar Scanner"
                  sh "mvn clean compile"
               withSonarQubeEnv('sonar-7') { 
                 sh "mvn sonar:sonar "
                }                     
          }
      }
	    
      stage('Unit Test Cases') {
         
          steps{
	       echo "Clean and Test"
              sh "mvn clean test"  
          }
          post{
              success{
		      echo "Clean and Test"
                  junit 'target/surefire-reports/*.xml'
              }
          }
      }
	    
      stage('Build Code') {
        
          steps{
	      unstash 'Source'
              sh "mvn clean package"  
          }
          post{
              success{
                  archiveArtifacts '**/*.war'
              }
          }
      }
	    
 
 
         
     stage ('Integration-Test') {
	
	steps {
             echo "Run Integration Test Cases"
             unstash 'Source'
            sh "mvn clean verify"
        }
    }
	    
     
     

    }
}
