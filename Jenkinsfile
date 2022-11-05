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
		 
	}
}
