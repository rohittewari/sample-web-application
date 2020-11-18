currentBuild.displayName = "Final_Demo # "+currentBuild.number

   def getDockerTag(){
        def tag = sh script: 'git rev-parse HEAD', returnStdout: true
        return tag
        }
 


pipeline{
	 // Assign to docker slave(s) label, could also be 'any'
        agent any  //{
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


		
              stage('build and push docker image')
                {
              steps{
                  script{
		   sh 'pwd'	  
		   sh 'cp -r ../MyPipeline@2/target .'
                   sh 'docker build . -t rohittew/devops-training:1.0'
		 //  withCredentials([string(credentialsId: 'docker_password', variable: 'docker_password')]) {
                 withCredentials([usernamePassword(credentialsId: 'docker_password', passwordVariable: 'docker-password-var', usernameVariable: 'docker-username')]) {				    
				  sh 'docker login -u $docker-username -p $docker-password-var'
				  sh 'docker push rohittew/devops-training:1.0'
			}
                       }
                    }
                 }
		
		
		
		
               }
	       
	       
	       
	      
    
}
