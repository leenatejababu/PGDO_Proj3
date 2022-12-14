node {
	def application = "devopsexample"
    
    //Its mandatory to change the Docker Hub Account ID after this Repo is forked by an other person
    def dockerhubaccountid = "vikidvg"
	
    // reference to maven
    // ** NOTE: This 'maven-3.5.2' Maven tool must be configured in the Jenkins Global Configuration.   
    def mvnHome = tool 'maven'

    // holds reference to docker image
    def dockerImage
 
    def dockerImageTag = "${dockerhubaccountid}/${application}:${env.BUILD_NUMBER}"
    
	stage('Clone Repo') { 
      // Get some code from a GitHub repository
      git url:'https://github.com/leenatejababu/PGDO_Proj3.git',branch:'main' //update your forked repo
      // Get the Maven tool.
      // ** NOTE: This 'maven-3.5.2' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven'
    } 
     stage('Build Project') {
      // build project via maven
      sh "'${mvnHome}/bin/mvn' clean install"
    }
	 stage('Build Docker Image with new code') {
      // build docker image
      dockerImage = docker.build("${dockerhubaccountid}/${application}:${env.BUILD_NUMBER}")
    }
	//push image to remote repository , in your jenkins you have to create the global credentials similar to the 'dockerHub' (credential ID)
    stage('Push Image to Remote Repo'){
	 echo "Docker Image Tag Name ---> ${dockerImageTag}"
	     docker.withRegistry('', 'dockerHub') {
             dockerImage.push("${env.BUILD_NUMBER}")
             dockerImage.push("latest")
            }
	}
} 
