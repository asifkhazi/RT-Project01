pipeline {
	agent any
	environment {
		Docker_Cred=credentials('docker_cred')
	}
	stages {
		stage ('SCM checkout') {
			agent {
          label 'new-node'
      }
			steps {
				  git branch:'main', url:'https://github.com/asifkhazi/RT-Project01.git'
				  stash(name: 'source', includes: '**/*.yaml')
			}
	  }
		stage('SonarQube analysis') {
		      	agent {
                		label 'new-node'
            }
      			steps {
				        withSonarQubeEnv(credentialsId: 'sonar-token') {
    					      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=sonarqube-example"
				        }
            }
    }
	}
}
