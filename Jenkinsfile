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
					sh "docker build . -t karumudi7/tomcatwebapp:${env.BUILD_ID}"
                                        sh "docker push karumudi7/tomcatwebapp:${env.BUILD_ID}"
				}
			}
		}		

		stage('Deploy') {
			steps
			{
                             //sh "docker service create --name tomcat-app tomcatwebapp:${env.BUILD_ID}"
                             sh "docker service update --replicas=5 --image karumudi7/tomcatwebapp:${env.BUILD_ID} tomcatapp"
                            
			}
		}
	}
}

