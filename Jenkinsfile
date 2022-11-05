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
		 
	}
}
