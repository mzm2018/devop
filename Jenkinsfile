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
		        docker.withRegistry('http://localhost:8085', 'nexusdockercredential') {
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
         build quietPeriod: 10, job: 'mzmtestpipeline'
	  }
      }
        }
        
     }
