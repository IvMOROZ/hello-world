node {
		stage('Checkout'){
				checkout scm
		}

		stage('build'){
				sh 'make'
		}

		stage ('Artifactory configuration, publish build info'){
				def server = Artifactory.newServer url: 'http://localhost:8081/artifactory', username: 'test_user', password: '18412654'
				// Read the upload spec which was downloaded from github.
				def uploadSpec = readFile 'upload.json'
				// Upload to Artifactory.
   			 	def buildInfo = server.upload spec: uploadSpec
				buildInfo.env.capture = true
				server.publishBuildInfo buildInfo
		}

	
}
