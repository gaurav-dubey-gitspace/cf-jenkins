pipeline {
	agent any
	
	stages {
		
		stage ('Build') {
		
			steps {
				withMaven(maven: 'maven_4_0_0') {
					sh 'mvn clean package'
				}
			}
		
		}
		
		stage ('Deploy') {
		
			steps {
				withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                                  credentialsId   : 'PCF_LOGIN',
                                  usernameVariable: 'USERNAME',
                                  passwordVariable: 'PASSWORD']]) {

                    sh '/usr/local/bin/cf login -a https://api.cf.us10.hana.ondemand.com -u $USERNAME -p $PASSWORD'
                    sh '/usr/local/bin/cf push'
                }
			}
		
		}
		
		
		
	}
}