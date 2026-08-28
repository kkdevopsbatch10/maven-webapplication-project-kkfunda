pipeline
{
 agent any
 tools
  {
    maven "maven-3.9.16"  
  }
  stages 
   {
    stages {
        // New Dedicated Metadata Stage
        stage('Set Build Identity') {
            steps {
                script {
                    // Overwrites the default build number (#45) in the left-hand sidebar history
                    currentBuild.displayName = "#${env.BUILD_NUMBER}"

                    // Sets the summary text on the specific build overview page
                    currentBuild.description = "Target: ${params.TARGET_ENV} | View Build Details: ${env.BUILD_URL}"
                }
            }
        }
     stage ('Git Checkout')
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
	    stage ('Deploy to tomcat')
	  {
	   steps
	    {
		
		sh """

      curl -u admin:Abhimanyu@3698 \
--upload-file /var/lib/jenkins/workspace/28082026-DWPL/target/maven-web-application.war \
"http://13.217.61.249:8089/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
		 
		}
	  }
   }//stage ending
}//pipeline ending 
