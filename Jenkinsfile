def revision = "1.0.${env.BUILD_ID}" 
pipeline{

agent any

tools{
maven 'maven3.8.2'

}


options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
}

stages{

  stage('CheckOutCode'){
    steps{
    git branch: 'master', credentialsId: 'gitcred', url: 'https://github.com/mmohammad786/maven-web-application.git'
	
	}
  }
  
  stage('MavenBuild'){
  steps{
  sh  "mvn clean package"
  }
  }
  stage('DockerBuild'){
  steps{
	  sh  "docker build -t mmohammad786/mavenwebapp:${revision} ."
  }
  }	
	
/*
 stage('ExecuteSonarQubeReport'){
  steps{
  sh  "mvn clean sonar:sonar"
  }
  }
  
  stage('UploadArtifactsIntoNexus'){
  steps{
  sh  "mvn clean deploy"
  }
  }
  
  stage('DeployAppIntoTomcat'){
  steps{
  sshagent(['bfe1b3c1-c29b-4a4d-b97a-c068b7748cd0']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.190.162:/opt/apache-tomcat-9.0.50/webapps/"    
  }
  }
  }
  */
}//Stages Closing

post{

 success{
 emailext to: 'moghalmohammad786@gmail.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'moghalmohammad786@gmail.com'
 }
 
 failure{
 emailext to: 'moghalmohammad786@gmail.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'moghalmohammad786@gmail.com'
 }
 
}


}//Pipeline closing
