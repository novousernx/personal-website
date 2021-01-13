pipeline {
		
		agent any
		
		environment {
				dockerImage = ''
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
		}
}
