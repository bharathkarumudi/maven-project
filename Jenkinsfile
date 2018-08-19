pipeline {
	agent any 
  tools {
    maven 'localMaven'
  }
	stages {

		stage('Build'){
			steps{
                                sh 'maven clean package'
                                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
			}

		}
	}
}
