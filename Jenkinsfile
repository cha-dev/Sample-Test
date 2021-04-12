pipeline{
agent any
tools{
 maven  "maven3.6.3"
}

 
 triggers{
 githubPush()
 }
 
 options{
 timestamps()
 buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '3', daysToKeepStr: '', numToKeepStr: '3'))
 }
 
 stages{
   stage('CheckoutCode')
   {
   steps{
    git credentialsId: 'f03e0c1d-ebf8-4473-a184-eef3ec8d96aa', url: 'https://github.com/cha-dev/Sample-Test.git'
   }
   }
 
   
    stage('Build')
    {
   steps{
    sh "mvn clean package"
   }
   }
   
   stage('ExecuteSonarQubeReportintotheSonarQubeServer')
    {
   steps{
    sh "mvn sonar:sonar"
   }
   }
   
   stage('Load into the Nexus')
    {
   steps{
    sh "mvn deploy"
   }
   }
   
   
}
}
