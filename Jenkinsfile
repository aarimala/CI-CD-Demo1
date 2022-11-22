pipeline {
	//def buildNumber = BUILD_NUMBER
  agent any
  
  tools
  {
	maven 'maven'
  }
  stages {
    stage ('SCM Checkout') {
      steps {
                //git branch: 'main', url: 'https://github.com/aarimala/CI-CD-demo.git'
	     git branch: 'main', url: 'https://github.com/aarimala/CI-CD-Demo1.git'
      }
      }
 stage ('Excute maven') {
      steps {
        sh 'mvn package'
      }
    }
	  	  stage ('docker build and tag') {
      steps {
        sh 'docker build -t my-webapp:latest .'
        sh 'docker tag my-webapp arifarimala/my-webapp:1.0'
      }
    }
    stage ('publish image to dockerhub') {
	 steps {
		 //withCredentials([string(credentialsId: 'MyDocker-Arif-ID', variable: 'dockerhub1')]) {
		 //withCredentials([sting(credentialsId: "MyDocker-Arif-ID",url: "arifarimala/my-webapp:1.0")]) {
		withCredentials([string(credentialsId: 'Docker_arif', variable: 'Docker_arif')]) {
		sh 'docker login -u arifarimala -p ${Docker_arif}'
		sh 'docker push arifarimala/my-webapp:1.0'
		}
		}
    }
	 stage ('Run Docker container on Jenkins Agent') {
		 steps {  
			 sh 'docker run -d -p 8030:8080 arifarimala/my-webapp:1.0'
               	
               		sshagent(['Ubuntu']) {
sh "ssh -o StrictHostKeyChecking=no ubuntur@35.154.204.177 'docker run -p 8030:8080 -d --name my-webapp arifarimala/my-webapp:1.0'"
				}	
         }  
	 }
  }
}
