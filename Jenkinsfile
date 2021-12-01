pipeline{

      agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.8.2/bin"
    }
        
        stages{

              stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('SonarScanner 2.14') { 
			      sh "mvn clean sonar:sonar"
                       	     	}
			      timeout(time: 1, unit: 'HOURS') {
			      def qg = waitForQualityGate()
				      if (qg.status != 'OK') {
					   error "Pipeline aborted due to quality gate failure: ${qg.status}"
				      }
                    		}
		    	    sh "mvn clean install"
		  
                 	}
               	 }  
              }	
		
            }	       	     	         
}
