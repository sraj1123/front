pipeline {
		agent any
		tools {
			nodejs "node"
      sonarqubeScanner 'SonarQubeScanner'
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
        stage('SonarQube analysis') {
                    steps {
                        script {
                            def scannerHome = tool name: 'SonarQube', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                            withSonarQubeEnv('SonarQube') {
                                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=Test3 -Dsonar.projectName=Test3"
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
