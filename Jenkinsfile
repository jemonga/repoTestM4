pipeline {
    agent any
    stages {
	   stage('Preparation') {
		   steps {
			   script {
		  		git 'https://github.com/jglick/simple-maven-project-with-tests.git'
		  		env.mvnHome = tool 'miMaven'
			   }
		   }
	   }
	   stage('Build') {
		   steps {
			   script {
				  env.JAVA_HOME="${tool 'jdk8'}"
				  env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
exit 1 //			   	  input "Continue?"
				  if (isUnix()) {
					 sh "'${env.mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
				  } else {
					 bat(/"${env.mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
				  }
			   }
		   }
	   }
	   stage('Results') {
		   steps {
			   script {
				  junit '**/target/surefire-reports/TEST-*.xml'
				  archive 'target/*.jar'
			   }
		   }
	   }
	   post {
		   always {
			   echo "Hemos terminado!"
		   }
	   }
    }
}
