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

		stage('Deploy_App') {
			steps
			{
				sh "docker container rm -f tomcat-app" 
				sh "docker container run -d --name tomcat-app -p 8082:8080 tomcatwebapp:${env.BUILD_ID}"
			}
		}
	}
}

