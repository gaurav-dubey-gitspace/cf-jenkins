pipeline {
	agent any
	tools{maven '3.8.4'}
	stages {
		stage ('Build') {
		
			steps {
				withMaven(maven: 'maven_3_8_4') {
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
