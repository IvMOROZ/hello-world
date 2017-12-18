node { 	
	agent { label 'test-slave' }
	stages {
		stage('Test_build'){
			steps {
				checkout scm
				sh 'make'
			      }
		}
	}		
}
