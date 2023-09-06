node {
    stage ('Git-Checkout') {
             git branch: 'main',
                credentialsId: 'github-token',
                url: 'https://github.com/suppu19/Jenkins-mvn-sonar.git'
                
            }
    stage ('Maven-build') {
                
            sh 'mvn clean package'
             archiveArtifacts artifacts: "**/target/*.jar"
        }
        

     stage("sonarbuild"){
            withSonarQubeEnv(credentialsId: 'newsonar') {
                sh "mvn sonar:sonar"
            }
                
        }
    stage("nexusrepo") {   
        nexusArtifactUploader artifacts: 
        [[artifactId: 'java-web-app', classifier: '', file: 'target/java-web-app-3.3.0-SNAPSHOT.jar', type: 'jar']], 
        credentialsId: 'nexus-login',
        groupId: 'com.example',
        nexusUrl: '3.110.41.150:8081', 
        nexusVersion: 'nexus3',
        protocol: 'http',
        repository: 'nexus-repo',
        version: '3.3.0-SNAPSHOT'
    }
}    
    
