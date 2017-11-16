pipeline {
    agent any

    stages {

	   stage('Preparation') { // for display purposes
		  // Get some code from a GitHub repository
		  git 'https://github.com/jglick/simple-maven-project-with-tests.git'
		  // Get the Maven tool.
		  // ** NOTE: This 'M3' Maven tool must be configured
		  // **       in the global configuration.           
		  env.mvnHome = tool 'miMaven'
	   }
	   stage('Build') {
		  // Run the maven build
		  env.JAVA_HOME="${tool 'jdk8'}"
		  env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
		  if (isUnix()) {
			 sh "'${env.mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
		  } else {
			 bat(/"${env.mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
		  }
	   }
	   stage('Results') {
		  junit '**/target/surefire-reports/TEST-*.xml'
		  archive 'target/*.jar'
	   }
    }
}
