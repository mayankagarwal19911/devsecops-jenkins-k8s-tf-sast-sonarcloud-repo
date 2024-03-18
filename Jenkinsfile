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
		withCredenstials([string(credentialsId: 'sonar-cloud-secret', variable: 'sonar-token')])
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=devsecops-pipeline-repo1 -Dsonar.organization=devsecops-pipeline-repo1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=${sonar-token}'
			}
        } 
  }
     stage('RunSCAAnalysisUsingSnyk') {
	    steps {
		withCredenstials([string(credentialsId: 'snyk-token', variable: 'SNYK_TOKEN')])
		sh 'mvn snyk:test -fn'
			}
	} 
  }
}
