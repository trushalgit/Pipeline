pipeline {
	agent any 
	
	stages {
	    stage('Checkout') {
	        steps {
			checkout scm			       
		      }}
		stage('Build') {
	           steps {
			  sh '/home/linux/maven/apache-maven-3.9.6/bin/mvn install'
                        }}
		stage('Deployment'){
		    steps {
		sh 'cp target/Pipeline.war /home/linux/maven/apache-tomcat-9.0.88/webapps'
                echo "deployment has been COMPLETED on QA!"
			 }}

}}
