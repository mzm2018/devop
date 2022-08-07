pipeline {
    agent any
      tools {
       maven 'maven'
	 	jdk 'java'
    }
     stages {
	stage('Build maven '){
		steps {
			sh 'pwd'
			sh 'mvn clean install package'
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
			def customImage = docker.build('localhost:8085/devopjava', "./docker")
		        docker.withRegistry('http://localhost:8085', 'nexusdockercredential') {
			customImage.push("latest")
		                    }
		         }
	              }
           }

        }
        
     }
