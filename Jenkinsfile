node 

{
   def mavenHome = tool name: 'maven' 
      
    // def mavenHome = tool name: 'maven3.8.5'
    stage ('checkoutstage-git') 
    {
      git credentialsId: '208b1c9d-f92c-4e69-8a0d-1b07fb8d233c', url: 'https://github.com/IBM-batch/maven-web-application2.git'  
    } //gitclosing
    
    stage ('buildautomationstage')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }  //buildstageclosing
    
    stage ('ExecuteSonarQubeReport')
    {
       sh "${mavenHome}/bin/mvn sonar:sonar"
   }   //scanning stage
   stage ('deployment-tomcat')
   {
    sshagent(['74458fca-6380-4214-9668-704c8b6d82a7']) {
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.34.10:/opt/apache-tomcat-9.0.102/webapps/"
    // some block
}
} //tomcat
} //nodeclosing
