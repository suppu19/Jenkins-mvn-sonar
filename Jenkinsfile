pipeline{
    agent any
    tools{

        maven 'mvn'

    }
        
    stages{
        stage("maven build"){
           steps{
            sh "mvn clean package"
     } 
                post {
                    success{ 
                        archiveArtifacts artifacts: '**/*.jar'

                    }
                }
        }    
    }
}            
           
        
    
