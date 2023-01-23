pipeline
{
    agent any
    stages
      {
        stage('ContinuousDownload')
          {
             steps
               {
                  git 'https://github.com/intelliqittrainings/maven.git'
               }
          }
        stage('ContinuousBuild')
          {
             steps
               {
                   sh 'mvn package'
               }
          }  
        stage('ContinuousDeployment')
          {
             steps
               {
                  deploy adapters: [tomcat9(credentialsId: '986ae753-77fb-4d82-86de-010a9bc00d3c', path: '', url: 'http://172.31.93.88:8080')], contextPath: 'testingapp', war: '**/*.war'
               }
          }
        stage('ContinuousTesting')
          {
             steps
               {
                  git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                  sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
                   
               }
          }
      }
    post
      {
        success
           {
              deploy adapters: [tomcat9(credentialsId: '986ae753-77fb-4d82-86de-010a9bc00d3c', path: '', url: 'http://172.31.84.207:8080')], contextPath: 'prodapp', war: '**/*.war'
           }
        failure
           {
              mail bcc: '', body: 'CI-CD FAILED', cc: '', from: '', replyTo: '', subject: 'ci-cd failed', to: 'sergeakak@yahoo.com'
           }
      }
          
 }
