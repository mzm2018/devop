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
			def customImage = docker.build('mzm1/devopjava', "./docker")
		        docker.withRegistry('', 'dockerhub') {
			customImage.push("latest")
		                    }
		         }
	              }
           }

        }
        
     }
