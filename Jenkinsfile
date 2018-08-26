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
                             //sh "docker service create --name tomcat-app tomcatwebapp:${env.BUILD_ID}"
                             sh "docker service update --image tomcatwebapp:${env.BUILD_ID} --replicas=8 tomcat-app"
			}
		}
	}
}

