node {
	stage('Clone Repo') { 
      // Get some code from a GitHub repository
      git url:'https://github.com/leenatejababu/PGDO_Proj3.git',branch:'main' //update your forked repo
      // Get the Maven tool.
      // ** NOTE: This 'maven-3.5.2' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven-3.5.2'
    }    
} 
