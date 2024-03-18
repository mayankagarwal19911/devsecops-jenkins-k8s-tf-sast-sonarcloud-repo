pipeline {
  agent any
  tools { 
        maven 'Maven_3.2.5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {
		withCredentials([string(credentialsId: 'sonar-cloud-secret', variable: 'sonar-token')]){
			sh "mvn clean verify sonar:sonar -Dsonar.projectKey=devsecops-pipeline-repo1 -Dsonar.organization=devsecops-pipeline-repo1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=${sonar-token}"
		}
	   }
    } 
     stage('RunSCAAnalysisUsingSnyk') {
	    steps {
		withCredentials([string(credentialsId: 'snyk-token', variable: 'SNYK_TOKEN')]){
			sh "mvn snyk:test -fn"
		}
	   }
    } 
  }
}
