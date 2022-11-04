pipeline {
	agent any
	tools {
        maven 'Maven 3.8.6'
	}
    
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
		 
	}
}
