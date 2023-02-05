pipeline {
   agent {
        label 'Slave1'
    }
    
        tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('SCM') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Dignity26/Java-mvn-app2'
				
				                
            }
		}
			
		stage('Build') {
            steps {
                
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
            
            }
		stage('Deploy to QA') {
            steps {
				script {
                
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Jenkins-QA', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'target/', sourceFiles: 'target/mvn-hello-world.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                
            }
			
			}
			post {
				success{
					sh "echo 'Send Email on success'"
					mail bcc: '', body: '"Please go to ${BUILD_URL} and verify the build"', cc: '', from: '', replyTo: '', subject: 'Job \'${JOB_NAME}\' (${BUILD_NUMBER})--Successful', to: 'im.ajitlende@gmail.com'
					
				}
				failure{
					sh "echo 'Send Email on failure'"
					mail bcc: '', body: '"Please go to ${BUILD_URL} and verify the build"', cc: '', from: '', replyTo: '', subject: 'Job \'${JOB_NAME}\' (${BUILD_NUMBER})--Failure', to: 'im.ajitlende@gmail.com'
					
				}
			}
			
            
            }


		}
		
		        
    }



