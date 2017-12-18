node('test-slave') {
		stage('Checkout'){
				checkout scm
		}
		stage('build'){
				sh 'make'
		}
}
