node {
		stage('Checkout'){
				checkout scm
		}

		stage('build'){
				sh 'make'
		}

		stage ('Artifactory configuration'){
				def server = Artifactory.server ART
				// Read the upload spec which was downloaded from github.
				def uploadSpec = readFile 'upload.json'
				// Upload to Artifactory.
   			 	def buildInfo = server.upload spec: uploadSpec
				buildInfo.env.capture = true
				server.publishBuildInfo buildInfo
		}

	
}
