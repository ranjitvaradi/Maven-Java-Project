
pipeline {
    agent any

    stages {
                   
	stage('SonarQube analysis') {
         
          steps{
                echo "Sonar Scanner"
                  sh "mvn clean compile"
               withSonarQubeEnv('Sonar') { 
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
