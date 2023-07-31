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
            
        stage("sonarbuild"){
            steps{
                script {
                    withSonarQubeEnv(credentialsId: 'sonarqubelogin') {
                        sh "mvn sonar:sonar"
                        }


                }  
            }
        }
       stage("nexus artifact") {
            steps{
                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'java-web-app', 
                                                        classifier: '', 
                                                        file: 'target/java-web-app-3.3.0-SNAPSHOT.jar', 
                                                        type: 'jar']],
                                                        credentialsId: 'nexus-login', 
                                                        groupId: 'com.example', 
                                                        nexusUrl: '13.127.218.104:8081', 
                                                        nexusVersion: 'nexus3', 
                                                        protocol: 'http', 
                                                        repository: 'nexus-repo', 
                                                        version: '3.3.0-SNAPSHOT'
                }
            }
       }       
            
    }
}           


           
        
    
