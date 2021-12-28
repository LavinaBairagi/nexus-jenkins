
node {
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
       git 'https://github.com/LavinaBairagi/nexus-jenkins.git'
        
    }
   
    stage('Build') {
                sh "mvn clean test"
    }
    
    stage('Package') {
                sh "mvn package"
    }
    
     stage('ansible-deploy'){
        
ansiblePlaybook(credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'ineventory.inv', playbook: 'download.yml')    
   }
     
    
   
    
    stage('Nexus') {
       nexusArtifactUploader artifacts: [[artifactId: 'nexus-jenkins',
 classifier: '', file: 'target/nexus-jenkins-0.0.1-SNAPSHOT.war',
 type: 'war']], credentialsId: 'nexus', groupId: 'com.jenkins.nexus', 
nexusUrl: 'localhost:8110', nexusVersion: 'nexus3',
 protocol: 'http', 
repository: 'maven-central-repository',
 version: '0.0.1'    }
 
 
  stage('Deploy') {
                bat "mvn deploy"
    }
    
 

}
