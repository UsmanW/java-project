properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git credentialsId: 'github-credential-assignment10', url: 'https://github.com/UsmanW/java-project'
		sh 'ant -f test.xml -v'   
        junit 'reports/*.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
}
