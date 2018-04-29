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
        s3CopyArtifact buildSelector: lastSuccessful(), excludeFilter: '', filter: 'rectangle-*.jar', flatten: false, optional: false, projectName: 'java-pipeline', target: 'http://usman-assignment-10.s3-website-us-east-1.amazonaws.com'
        }
    stage ('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
        }
    }   
}
