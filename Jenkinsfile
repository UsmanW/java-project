properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git credentialsId: 'github-credential-assignment10', url: 'https://github.com/UsmanW/java-project'
		sh 'ant -buildfile test.xml'   
	}   
	stage('Build') {    
		sh 'ant'   
	}   
	stage('Results') {    
		junit 'reports/*.xml'   
	}
}
