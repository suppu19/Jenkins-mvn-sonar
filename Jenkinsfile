pipeline{
    agent any
    tools{

        maven 'mvn'

    }
        
    stages{
        stage("maven build"){
           steps{
            sh "mvn clean pacage"
     } 
                post {
                    sucess{ 
                        archiveArtifacts artifacts: '**/*.jar'

                    }
                }
        }    
    }
}            
           
        
    
