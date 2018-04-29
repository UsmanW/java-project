properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Test') {    
		git credentialsId: 'github-credential-assignment10', url: 'https://github.com/UsmanW/java-project'
		sh 'ant -f test.xml -v'   
        junit 'reports/*.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}
    stage ('Deploy'){
        s3Upload consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'usman-assignment-10', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '*.jar', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'jenkins', userMetadata: []
        }
    stage ('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
        }
    }   
}

