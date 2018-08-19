pipeline {
	agent any 
  
  tools {
    maven 'localMaven'
  }
	stages {

		stage('Build') {
			steps {
                 sh 'mvn clean package'               
             }

			post {
				success{
					sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
				}
			}
		}		

		stage('Deploy') {
			steps
			{
				sh "docker service update --image --replicas=5 tomcatwebapp:${env.BUILD_ID} tomcat-app"
			}
		}
	}
}

