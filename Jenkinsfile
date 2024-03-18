pipeline {
  agent any
  tools { 
        maven 'Maven_3.2.5'  
    }
   environment {
     SONAR_TOKEN = credentials('sonar-cloud-secret')
   }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=devsecops-pipeline-repo1 -Dsonar.organization=devsecops-pipeline-repo1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=${SONAR_TOKEN}'
	   }
    } 
     stage('RunSCAAnalysisUsingSnyk') {
	    steps {
		withCredentials([string(credentialsId: 'snyk-token', variable: 'SNYK_TOKEN')]){
			sh 'mvn snyk:test -fn'
		}
	   }
    } 
  }
}
