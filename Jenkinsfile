pipeline {
  agent any
  tools {
    maven "maven-stephanie"
  }
  stages {
    stage ('Maven Clean'){
      steps{
        sh 'mvn clean'
      }
    }
    stage ('Maven package') {
      steps{
        sh 'mvn package'
      }
    }
    stage('sonarqube analysis and testing'){
      steps{
        script{
          withSonarqubeEnv('sonarqube'){
            sh'mvn clean package sonar:sonar'
          }
        }
      }
    }
    stage('quality gate'){
      steps{
        script{
          timeout(time: 1, unit 'hours'){
            def qg =waitqualitygate()
            if (qg.status != 'ok') {
              error 'pipeline aborted due to quality gate failure: ${qg.status}'
            }
          }
        }
      }
    }
    
   stage ('Docker build and push'){
     steps{
       withDockerRegistry([ credentialsId: "docker_creds", url: "https://index.docker.io/v1/" ]){
     sh 'docker build -t constanceavouzoa1/java-maven . -f Dockerfile'
     sh 'docker push constanceavouzoa1/java-maven' 
  }
}
   }  
    
    
    
    
    
    
    
    
    
  }
}
  
     
              
              
              
              
              
              
              
              
 
  

              
              
              
  
    
      
  
              
              
              
              
              
              
              
              
              
  

              
            
      
             

    
 
  
                                 
                                 
                                 
                                 

                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
