pipeline {
		agent any
		tools {
			nodejs "node"
		}
		stages {
				stage('Git Clone') {
				steps {
					// Get code from a GitHub repository
					git branch: 'master', url: 'https://github.com/sraj1123/front'
					}
				}
				stage('NPM Build') {
				steps {
					script {
					// Build npm Code
					sh "npm install"
                    			sh "npm run build"
						}
					}
				}
				stage('Sonar Scan') {
					steps {
						script {
						withSonarQubeEnv(credentialsId: 'SonarQube_Token') {
              sh "${env.SONARQUBE_SCANNER_HOME}/bin/sonar-scanner"
						  sh 'sonar-scanner -Dsonar.projectName=Test3 -Dsonar.projectKey=Test3'
              
								}
							}
						}
					}
				stage('Quality Gate Check') {
					steps {
						timeout(time: 1, unit: 'HOURS') {
							waitForQualityGate abortPipeline: true
							}
						}
					}   
			}
	}
