/* pipeline{

agent any

tools{
maven 'maven3.8.2'

}

triggers{
pollSCM('* * * * *')
}

options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
}

stages{

  stage('CheckOutCode'){
    steps{
    git branch: 'development', credentialsId: '957b543e-6f77-4cef-9aec-82e9b0230975', url: 'https://github.com/devopstrainingblr/maven-web-application-1.git'
	
	}
  }
  
  stage('Build'){
  steps{
  sh  "mvn clean package"
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
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
 failure{
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
}


}//Pipeline closing   */


node {
            def mavenHome = tool name: "maven-3.9.10"
     echo "the job name is $job_name"
     echo "the current build number is:$build_number "
    stage("Checkout from Git") {
        git branch: 'main', credentialsId: '264d3b9f-b903-49d4-abb0-07e1c52aaa45', url: 'https://github.com/harsha0620/maven-web-application.git'
    }

    stage("Build") {
        sh "${mavenHome}/bin/mvn clean package"
    }

    stage("Code Coverage") {
        jacoco()
    }

    /*
    stage("Execute Sonar Report") {
        withSonarQubeEnv("sonarqubeserver") {
            sh "${mavenHome}/bin/mvn sonar:sonar"
        }
    }

    stage("Push Artifact to Nexus") {
        nexusArtifactUploader(
            artifacts: [[
                artifactId: 'maven-web-app',
                classifier: '',
                file: 'target/maven-web-app.war',
                type: 'war'
            ]],
            credentialsId: 'fcbfa5aa-9d63-4ec0-a75d-94c0d70bf5d2',
            groupId: 'neususer',
            nexusUrl: '34.172.209.178:8081',
            nexusVersion: 'nexus2',
            protocol: 'http',
            repository: 'maven-web-application',
            version: '1.0-SNAPSHOT'
        )
    }
    */
}
