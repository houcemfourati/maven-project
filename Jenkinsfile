pipeline{
agent any

parameters{
string(name: 'tomcat_dev',
defaultValue: 'C:\prog\apache-tomcat-8.5.73\webapps',
description:'Staging Server : 8080')
string(name:'tomcat_prod',
defaultValue:'C:\prog\apache-tomcat-8.5.73_prod\webapps',
description: 'Production Server : 9090)
}

triggers {
pollSCM('* * * * *')
}

stages{
	stage('Build'){
	steps{
	bat 'mvn clean package'
	}
	post{
	success{
	echo "Now Archiving ...."
	archiveArtifacts artifacts: '**/target/*.war'
	}
	}
	}
	
	stage('Deployments'){
	parallel {
	stage ('Deploy to Staging){
	steps {
	bat "cp **/target/*.war %tomcat_prod%"
	}
	}}}}
	
	
	
}
