pipeline
{
  agent any
  tools
  {
   maven "maven-3.9.16"
  }
  stages
  {
    stage ('git checkout')
    {
     steps 
	  {
	  git branch: 'master', url: 'https://github.com/kkdevopsbatch10/maven-webapplication-project-kkfunda.git'
	  }
    }
	stage ('Compile')
    {
     steps 
	 {
	  sh "mvn compile"
	 }
    }
	stage ('Build')
    {
     steps 
	 {
	  sh "mvn clean package"
	 }
    }
	stage ('SQ Report')
    {
     steps 
	 {
	  sh "mvn sonar:sonar"
	 }
    }
	stage ('Nexus Report')
    {
     steps 
	 {
	  sh "mvn deploy"
	 }
    }
  }// Stages Ending
}//PipiLine Ending



