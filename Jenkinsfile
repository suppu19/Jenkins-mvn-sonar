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
                    //def nexus_url 
                    //def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "nexus-repo-snapshot" : "nexus-repo-release"
                     pom = readMavenPom file: 'pom.xml'
                    
                    nexusArtifactUploader artifacts: [[artifactId: "${pom.artifactId}", //'java-web-app', 
                                                        classifier: '', 
                                                        file: "target/${pom.artifactId}-${pom.version}.jar",//'target/java-web-app-3.3.0-SNAPSHOT.jar', 
                                                        type: "${pom.packaging}" ] //'jar'
                                                        ],
                                                        credentialsId: 'nexus-login', 
                                                        groupId: "${pom.groupId}", //'com.example' 
                                                        nexusUrl: "13.127.218.104:8081", //"${env.nexus-ip}", 
                                                        nexusVersion: 'nexus3', 
                                                        protocol: 'http', 
                                                        repository: 'nexus-repo', 
                                                        version:"${pom.version}" //'3.3.0-SNAPSHOT'
                }
            }
      }       
            
    }
}           


           
        
    
