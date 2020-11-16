currentBuild.displayName = "Final_Demo # "+currentBuild.number

   def getDockerTag(){
        def tag = sh script: 'git rev-parse HEAD', returnStdout: true
        return tag
        }
 


pipeline{
	 // Assign to docker slave(s) label, could also be 'any'
        any agent //{
         //label 'docker' 
       // } 
	
        environment{
	    Docker_tag = getDockerTag()
        }
        
        stages{
              stage('Quality Gate Status Check'){
               // def dockerHome = tool 'docker'
               // env.PATH = "${dockerHome}/bin:${env.PATH}"
               agent {			    
                docker {
		// Set both label and image
               // label 'docker'	
                image 'maven'
                args '-v $HOME/.m2:/root/.m2'
                }
            }
                  steps{
                      script{                  
                
		    sh "mvn clean install"
                  }
                }  
              }


		
               }
	       
	       
	       
	      
    
}
