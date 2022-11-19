pipeline {
  agent any
  
  tools
  {
	maven 'Maven'
  }
  stages {
    stage ('SCM Checkout') {
      steps {
                //git branch: 'main', url: 'https://github.com/aarimala/CI-CD-demo.git'
	      git branch: 'main', url: 'https://github.com/aarimala/CI-CD-demo.git'
      }
      }
 stage ('Excute Maven') {
      steps {
        sh 'mvn package'
      }
    }
  }
}
