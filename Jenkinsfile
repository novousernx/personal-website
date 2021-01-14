pipeline {
		
		agent any
		
		environment {
				dockerImage = ''
				registry = 'novousernx/personal-website'
				registryCredential = 'dockerhub'
		}
		
		stages {
				stage('Checkout') {
						steps {
								checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/novousernx/personal-website.git']]])
						}
				}
				
				stage('Build Docker Image') {
						steps {
								script {
										dockerImage = docker.build registry
								}
						}
				}
				
				stage('Upload To DockerHub') {
						steps {
								script {
										docker.withRegistry( '' , registryCredential) {
												dockerImage.push()
										}
								}
						}
				}
		}
}
