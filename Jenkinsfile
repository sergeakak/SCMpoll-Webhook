pipeline
{
    agent any
    stages
      {
        stage('ContinuousDownload')
          {
             steps
               {
                  git 'https://github.com/sergeakak/SCMpoll-Webhook.git'
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



pipeline
{
  agent any
  stages
    {
      stage('ContinuousDownload') 
        {
            steps
              {
                script
                  {
                    try
                    {
                      git 'https://github.com/intelliqittrainings/maven.git' 
                    }
                    catch(Exception e1)
                    {
                      mail bcc: '', body: 'download failed', cc: '', from: '', replyTo: '', subject: 'ci-cd download', to: 'GITteam@gmail.com' 
                      exit(1)
                    }
                 }
              }
        }
        stage('ContinuousBuild') 
        {
            steps
              {
                script
                  {
                    try
                    {
                       sh 'mvn package' 
                    }
                   catch(Exception e2)
                   {
                      mail bcc: '', body: 'download failed', cc: '', from: '', replyTo: '', subject: 'ci-cd download', to: 'GITteam@gmail.com' 
                      exit(1) 
                   }
                 }
              }
        }
        stage('ContinuousDeployment') 
        {
            steps
              {
                script
                  {
                    try
                    {
                       deploy adapters: [tomcat9(credentialsId: '986ae753-77fb-4d82-86de-010a9bc00d3c', path: '', url: 'http://172.31.93.88:8080')], contextPath: 'testingapp', war: '**/*.war' 
                    }
                   catch(Exception e3)
                   {
                      mail bcc: '', body: 'download failed', cc: '', from: '', replyTo: '', subject: 'ci-cd download', to: 'GITteam@gmail.com' 
                      exit(1)
                   }
                 }
              }
        }
        stage('ContinuousTesting') 
        {
            steps
              {
                script
                  {
                    try
                    {
                      git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                      sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'  
                    }
                   catch(Exception e4)
                   {
                      mail bcc: '', body: 'download failed', cc: '', from: '', replyTo: '', subject: 'ci-cd download', to: 'GITteam@gmail.com' 
                      exit(1)
                   }
                 }
              }
        }
        stage('ContinuousDelivery') 
        {
            steps
              {
                script
                  {
                    try
                    {
                      deploy adapters: [tomcat9(credentialsId: '986ae753-77fb-4d82-86de-010a9bc00d3c', path: '', url: 'http://172.31.84.207:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                   catch(Exception e5)
                   {
                      mail bcc: '', body: 'download failed', cc: '', from: '', replyTo: '', subject: 'ci-cd download', to: 'GITteam@gmail.com' 
                   }
                 }
              }
        }
    }
}
