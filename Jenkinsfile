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
/*
				  if (isUnix()) {
					 sh "'${env.mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
				  } else {
					 bat(/"${env.mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
				  }
*/
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
    }
   post {
	   always {
		   echo "Hemos tardado ${currentBuild.durationString}"
	   }
	   failure {
		echo "Algo ha fallado"
		mail to: 'jesusmg@meta4.com',
		subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
		body: "Something is wrong with ${env.BUILD_URL}"
	   }
	   changed {
		echo "Algo ha cambiado"
		mail to: 'jesusmg@meta4.com',
		subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
		body: "Something has changed with ${env.BUILD_URL}"
	   }
   }
}
