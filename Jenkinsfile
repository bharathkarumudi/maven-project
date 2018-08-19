pipeline {
	agent any 
  tools {
    maven 'localMaven'
  }
	stages {

		stage('Build')
		{
			steps
			{
                 sh 'mvn clean package'               
			}

			post {
				success{
					sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
				}

				stage('Deploy to staging') 
				{
					sh "docker container rm -f tomcatapp"
					sh "docker container run -d -name tomcatapp -p 8082:8080 tomcatwebapp:${env.BUILD_ID}"	
				}
			}
		}
	}
}
