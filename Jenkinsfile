properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		git credentialsId: 'github-credential-assignment10', url: 'https://github.com/UsmanW/java-project'
		sh 'ant -f test.xml -v'   
        junit 'reports/*.xml'
	}   
}
