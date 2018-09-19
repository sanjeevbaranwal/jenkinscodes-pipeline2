pipeline {
    agent {
     label 'linux-pool' 
    }
    
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
