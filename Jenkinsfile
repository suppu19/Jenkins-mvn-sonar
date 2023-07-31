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
                  def pom = readMavenPom file: 'pom.xml' 
                    
                    def nexusRepoName = Pom.version.endsWith("SNAPSHOT") ? "nexus-repo-snapshot" : "nexus-repo-release"
                    
                    nexusArtifactUploader artifacts: [[artifactId: 'java-web-app', 
                                                        classifier: '', 
                                                        file: 'target/java-web-app-3.3.0-SNAPSHOT.jar', 
                                                        type: 'jar']],
                                                        credentialsId: 'nexus-login', 
                                                        groupId: 'com.example', 
                                                        nexusUrl: 'nexus-ip', 
                                                        nexusVersion: 'nexus3', 
                                                        protocol: 'http', 
                                                        repository: 'nexus-repo', 
                                                        version: '3.3.0-SNAPSHOT'
                }
            }
       }       
            
    }
}           


           
        
    
