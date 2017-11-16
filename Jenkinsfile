pipeline {
    agent any

    stages {

	   stage('Preparation') {
		  git 'https://github.com/jglick/simple-maven-project-with-tests.git'
		  env.mvnHome = tool 'miMaven'
	   }
	   stage('Build') {
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
