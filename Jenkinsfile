pipeline {

 
agent any

 
//environment

 //	{

 
//	dockerImage = ''

 
//	registry='sushmitamukherjee/our-web-app'

 
//	registryCredential='dockerhub'

 
//	}

 


 
 

 
stages {

 
stage('Fetch')

 
{

 
steps

 
{

 
git url : "https://github.com/sushmita119/docker.git"

 
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
	
stage('Build Image')
{
steps
{
bat "docker build -t sushmitamukherjee/docker:${BUILD_NUMBER} ."
}
}
//stage("Cleaning Previous Deployment")
//{
//steps
//{
//catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE')
//{
//bat "docker stop assignmentdevcontainer"
//bat "docker rm -f assignmentdevcontainer"
//}
//}
//}
stage('Uploading Image')
           {
               steps
               {
                  bat "docker login -u sushmitamukherjee -p Uttam@@00ngr"
                   
                   //bat "docker tag nishant058/helloworld nishant"

 

 

 

                   bat "docker push sushmitamukherjee/docker:${Build_number}"
               }
           }
stage('Docker Run')
           {
               steps
               {
                  // bat "docker pull nishant058/helloworld"
                   bat " docker rm --force sushmitacontainer"
                   bat "docker run -d --name sushmitacontainer -p 9080:8080 sushmitamukherjee/docker:${Build_number}"

 

 

 

                   
               }
           }


}
}
 

 

}
