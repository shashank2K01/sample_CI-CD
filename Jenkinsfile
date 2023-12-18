pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'jdk8'
    }
    stages {      
        stage('Build maven') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('shashankadiga/samplecicd', "./docker")
                 docker.withRegistry('https://registry.hub.docker.com', 'docker_id') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
