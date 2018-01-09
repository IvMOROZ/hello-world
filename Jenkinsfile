node('test-slave') {
		stage('Checkout'){
				checkout scm
		}

		stage('build'){
				sh 'make'
		}

		stage ('Artifactory configuration'){
				def server = Artifactory.newServer 'ART'
				def artifactoryMaven = Artifactory.newMavenBuild()
				artifactoryMaven.tool = 'M3' // Tool name from Jenkins configuration
				artifactoryMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
				artifactoryMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server
				def buildInfo = Artifactory.newBuildInfo()
				buildInfo.env.capture = true
		}
		
		stage ('Exec Maven'){
				artifactoryMaven.run pom: 'maven-example/pom.xml', goals: 'clean install', buildInfo: buildInfo
		}

		stage ('Publish build info'){
				server.publishBuildInfo buildInfo
		}
}
