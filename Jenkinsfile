pipeline {
		agent any
		environment {
				DOCKER_TAG = getDockerTag()
		}
		stages {
				stage('Build Docker Image') {
						steps {
								sh "docker build . -t novousernx/personal-website:${DOCKER_TAG}"
						}
				}
				stage('DockerHub Push') {
						steps {
								withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dhpwd', usernameVariable: 'dhuser')]) {
    								sh "docker login -u ${dhuser} -p ${dhpwd}"
    								sh "docker push novousernx/personal-website:${DOCKER_TAG}"
    						}
						}
				}
		}
}

def getDockerTag() {
		def tag = sh script: 'git rev-parse HEAD', returnStdout: true
		return tag
}
