properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git credentialsId: 'testingCredentials', url: 'https://github.com/UsmanW/java-project.git'
		sh 'ant -buildfile test.xml'   
	}   
	stage('Build') {    
		sh 'ant'   
	}   
	stage('Results') {    
		junit 'reports/*.xml'   
	}
}

