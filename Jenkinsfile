pipeline{
    agent any
    tools{

        maven 'mvn'

    }
        
    stages{
        stage("maven build"){
           steps{
            sh "mvn clean package"
             archiveArtifacts artifacts: "**/*.jar"
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
                    //def nexus_url 
                    //def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "nexus-repo-snapshot" : "nexus-repo-release"
                     pom = readMavenPom file: 'pom.xml'
                    
                    nexusArtifactUploader artifacts: 
                                        [[artifactId: "${pom.artifactId}", 
                                        classifier: '', 
                                        file: "target/${pom.artifactId}-${pom.version}.jar",
                                        type: "${pom.packaging}" ] ],
                                        credentialsId: "nexus-login", 
                                        groupId: "${pom.groupId}", 
                                        nexusUrl: "13.127.218.104:8081", 
                                        nexusVersion: "nexus3", 
                                        protocol: "http", 
                                        repository: "nexus-repo", 
                                        version:"${pom.version}" //'3.3.0-SNAPSHOT'
                }
            }
      }       
            
    }
}           


           
        
    
