pipeline{
    agent any
    tools
        maven
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
           
        
    
