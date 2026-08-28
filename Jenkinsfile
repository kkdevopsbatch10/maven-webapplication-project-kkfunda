pipeline {
    agent any
    
    tools {
        maven "maven-3.9.16"  
    }
    
    stages {
        stage('Set Build Identity') {
            steps {
                script {
                    currentBuild.displayName =  "AXA-${env.BUILD_NUMBER}"
                }
            }
        }
        
        stage('Git Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/kkdevopsbatch10/maven-webapplication-project-kkfunda.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('SQ Report') {
            steps {
                sh "mvn sonar:sonar"
            }
        }
        
        stage('Nexus Report') {
            steps {
                sh "mvn deploy"
            }
        }
        
        stage('Deploy to tomcat') {
            steps {
                sh """
                    curl -u admin:Abhimanyu@3698 \
                    --upload-file /var/lib/jenkins/workspace/28082026-DWPL/target/maven-web-application.war \
                    "http://13.217.61.249:8089/manager/text/deploy?path=/maven-web-application&update=true"
                """
            }
        }
    } // Closes stages
} // Closes pipeline
