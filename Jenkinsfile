pipeline {
    agent {
     label 'linux-pool' 
    }
    
    parameters {
	 string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
	 string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
	 string(name: 'bname', defaultValue: '1.2', description: 'Environment build Variable')
    }
    
    triggers {
         pollSCM('* * 1 * *')
     }
    
    tools { 
        maven 'Maven 3.3.9' 
     }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
	       
		//sh "${mvnHome}/bin/mvn versions:set -DnewVersion=$bname.${env.BUILD_NUMBER}.${env.BUILD_TIMESTAMP}"
		//sh "${mvnHome}/bin/mvn package"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
