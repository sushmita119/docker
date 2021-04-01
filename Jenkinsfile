pipeline {

 
agent any

 
environment

 	{

 
	dockerImage = ''

 
	registry='sushmitamukherjee/our-web-app'

 
	registryCredential='dockerhub'

 
	}

 


 
 

 
stages {

 
stage('Fetch')

 
{

 
steps

 
{

 
git url : "https://github.com/sushmita119/our-first-app.git"

 
}

 
}

 
stage('Build')

 
{

 
steps

 
{

 
echo 'Hello World'

 
echo 'Building.....'

 
bat 'mvn clean install'

 
}

 
}

 
stage('Unit Test')

 
{

 
steps

 
{

 
echo 'Testing....'

 
bat 'mvn test'

 
}

 
}

 
stage('Sonar Analysis')

 
{

 
steps

 
{

 
echo 'Sonar Analysis....'

 
withSonarQubeEnv("sonar")

 
{

 
bat "mvn sonar:sonar"

 
}

 
}

 
}
stage('Upload to Artifactory')
        {
	        steps
	        {
			echo 'Uploading....'
		        rtMavenDeployer (
    			    id: 'deployer-unique-id',
		            serverId: 'Artifactory',
		            releaseRepo: 'example-repo-local',
		            snapshotRepo: 'example-repo-local' 
		        )
		        rtMavenRun (
		        pom: 'pom.xml',
		        goals: 'clean install',
		        deployerId: 'deployer-unique-id' 
		        )
		        rtPublishBuildInfo (
		            serverId: 'Artifactory' 
		                )
	        }
	     }

 

 
stage('Docker Image'){

 
steps{

 
script

 
{

 
dockerImage = docker.build registry

 
}

 
}

 
}

 
stage('Uploading Image')

 
{

 
steps

 
{

 
script

 
{

 
docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {

 
 

 
/* Push the container to the custom Registry */

 
dockerImage.push()

 
}

 
}

 
}

 
}

 
}

 
}
