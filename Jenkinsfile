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
			def customImage = docker.build('devopjava', "./docker")
		        docker.withRegistry('http://192.168.1.19:8085', 'nexusdockercredential') {
			customImage.push("latest")
		                    }
		         }
	              }
           }
     stage('Remove Unused docker image') {
      steps{
         sh "docker rmi devopjava:latest"
	  }
      }
	   stage('build new job') {
      steps{
         build job: 'downstreamjob', parameters: [string(name: 'BUILDNUMBER', value: env.BUILD_NUMBER)]
	  }
      }
        }
        
     }
