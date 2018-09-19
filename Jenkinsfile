pipeline {
    agent linux-pool

	parameters {
	 string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
	 string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
 }

	triggers {
		 pollSCM('* * * * *')
 }
	
	
	
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
			def mvnHome = tool 'mvn'
		    sh "${mvnHome}/bin/mvn versions:set -DnewVersion=$bname.${env.BUILD_NUMBER}.${env.BUILD_TIMESTAMP}"
		    sh "${mvnHome}/bin/mvn package"
				
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
			    parallel 'test': {
				  //sh "${mvnHome}/bin/mvn test; sleep 2;"
			      }, 'verify': {
				  //sh "${mvnHome}/bin/mvn verify; sleep 3"
			      }
            }
        }
		
		stage('Archive') {
			steps {
				echo 'Deploying....'
			}
		}
		}
		
		
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
