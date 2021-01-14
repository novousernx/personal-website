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
								withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
    								sh "docker login -u novousernx --password-stdin ${dockerhubpwd}"
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
