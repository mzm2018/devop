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
			customImage.push("${env.BUILD_NUMBER}")
		                    }
		         }
	              }
           }
     stage('Remove Unused docker image') {
      steps{
	      sh "docker rmi mzm1/devopjava:${env.BUILD_NUMBER}"
	  }
      }
	   stage('build new job') {
      steps{
         build job: 'downstreamjob', parameters: [string(name: 'BUILDNUMBER', value: env.BUILD_NUMBER)]
	  }
      }
        }
        
     }
