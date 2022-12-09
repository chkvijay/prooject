pipeline {
	agent any
    
	 stages {
		stage('git checkout'){
		     steps {
			    git 'https://github.com/chkvijay/prooject.git'
			   }
		}
		 stage('Unit testing'){
		     steps {
			    sh 'mvn test'
			   }
		}
		  stage('Integration testing'){
		     steps {
			    sh 'mvn verify -DskipUnitTests'
			   }
		}
		 stage('Maven Build'){
		     steps {
			    sh 'mvn clean install'
			   }
		}
		 stage('Static Code Analysis'){
		     steps {
			    script{
			    withSonarQubeEnv(credentialsId: 'sonar-api') {
   				sh 'mvn clean package sonar:sonar'
					}
			   }
		     	  }
			}
		 
		 stage('Quality Gate status'){
		     steps {
			     script {
			    	waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
			          }
			   }
		   }
		 
		 stage('artifact upload to nexus repository'){
		    steps {
		        script {
		         def readPomVersion = readMavenPom file : 'pom.xml'
		         
		         def nexusrepo = readPomVersion.version.endsWith("SNAPSHOT") ? "demo-snapshot" : "demoapp-release"
				
		nexusArtifactUploader artifacts: 
                [
                 [ 
                    artifactId: 'maven-project', 
                    classifier: '', 
                    file: 'webapp/target/webapp.war', 
                    type: 'war'
                 ]
                ],
                credentialsId: 'nexus-auth', 
                groupId: 'com.example', 
                nexusUrl: 'localhost:8085', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: nexusrepo, 
                version: "${readPomVersion.version}"
		       }
		    }
		    
		}
}
}
