currentBuild.displayName = "Final_Demo # "+currentBuild.number

   def getDockerTag(){
        def tag = sh script: 'git rev-parse HEAD', returnStdout: true
        return tag
        }
 
def dockerHome = tool 'docker'
env.PATH = "${dockerHome}/bin:${env.PATH}"

pipeline{
        agent any  
        environment{
	    Docker_tag = getDockerTag()
        }
        
        stages{


              stage('Quality Gate Status Check'){

               agent {
			    
                docker {				
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
