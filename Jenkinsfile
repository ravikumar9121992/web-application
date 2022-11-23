pipeline {
    agent any
    tools {
        maven 'Maven'
        
    }
    
    stages { 

    
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
        
        
         stage('build') {
            steps {
                sh 'mvn install package'
                
            }
        }

    
   /*     
 stage('Build'){
  steps{
   sh  "mvn clean package"
  }
  }    
 
 stage('SonarQube'){
   steps{
      sh  "mvn clean sonar:sonar"
  }
    }
  
  stage('nexus'){
    steps{
         sh  "mvn clean deploy"
 }
   }
  */    

stage('Build Docker Image'){
            steps{
                 sh 'docker build -t awsdocker123456789/spring-boot-mongo .'
                 sh 'docker build -t tomcat:${BUILD_NUMBER} .'
                 sh 'docker run -itd --name sita -p 285:8080 tomcat:${BUILD_NUMBER}'

             }
         }
        stage('Push Docker Image'){
             steps{
                     withCredentials([usernamePassword(credentialsId: 'DOCKER_HUB_CREDENTIALSi', passwordVariable: 'DOCKER_HUB_CREDENTIALSp', usernameVariable: 'DOCKER_HUB_CREDENTIALSu')]) {

                      sh "docker login -u awsdocker123456789 -p Awsdocker123"
            }
            sh 'docker push awsdocker123456789/spring-boot-mongo tomcat:${BUILD_NUMBER}'
        }
      }
        
        
    }
}
