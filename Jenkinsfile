pipeline {
	agent any
	environment {
		Docker_Cred=credentials('docker_cred')
	}
	tools {
		maven 'maven'
	}
	stages {
		stage ('SCM checkout') {
			agent {
          			label 'new-node'
     			}
			steps {
				  git branch:'main', url:'https://github.com/asifkhazi/RT-Project01.git'
				  stash(name: 'source', includes: '**/*.yaml')
				  sh 'mvn --version'
			}
	  	}
		stage('SonarQube analysis') {
		      	agent {
                		label 'new-node'
            		}
			environment { SCANNER_HOME = tool 'sonar-scanner'}
      			steps {
				withSonarQubeEnv('SanrQubeServer') {
    					sh "${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=sonarqube-example"
				}
            		}
   	 	}
	}
}
