pipeline {
	agent any 
	
	parameters {
                  choice choices: ['DEV', 'QA', 'UAT'], name: 'ENV'
                 }
	
	stages {
	    stage('Checkout') {
	        steps {
			checkout scm			       
		      }}
		stage('Build') {
	           steps {
			  sh '/home/devops/installers/apache-maven-3.9.6/bin/mvn install'
		   }}
		stage('Deployment'){
		    steps {
			script {
			 if ( env.ENV == 'DEV' ){
        	sh 'cp target/Pipeline.war /home/devops/installers/apache-tomcat-9.0.88/webapps'
        	echo "deployment has been COMPLETED on Dev!"
			 }
			else if ( env.ENV == 'QA' ){
    		sh 'cp target/Pipeline.war /home/devops/installers/apache-tomcat-9.0.88/webapps'
    		echo "deployment has been done on QA!"
			}
			}}}	
		stage('slack-notification'){
		   steps {
		     
                   slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#devops-slack', color: 'good', message: 'Welcome', teamDomain: 'contoso', tokenCredentialId: '6bbc0d9c-5ccb-4126-9738-9f4ed8ae5105'		     
		   }}	
}}
