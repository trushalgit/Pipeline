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
			  sh '/home/linux/installers/apache-maven-3.9.6/bin/mvn install'
		   }}
		stage('Deployment'){
		    steps {
			script {
			 if ( env.ENV == 'DEV' ){
        	sh 'cp target/Pipeline.war /home/linux/installers/apache-tomcat-9.0.88/webapps'
        	echo "deployment has been COMPLETED on Dev!"
			 }
			else ( env.ENV == 'UAT' ){
    		sh 'cp target/Pipeline.war /home/linux/installers/apache-tomcat-9.0.88/webapps'
    		echo "deployment has been done on UAT!"
			}
			}}}	
}}
