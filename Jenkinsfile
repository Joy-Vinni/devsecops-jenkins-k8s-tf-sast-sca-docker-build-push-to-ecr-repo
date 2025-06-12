pipeline {
  agent any
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		        echo "Before Mvn "
		        sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=isuydsshduyasguiasgfuvf -Dsonar.organization=isuydsshduyasguiasgfuvf -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=d8486dddffb4417cfb282197cf0f458773612dc7'
                echo "after mvn run"
            }
        } 

	stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("asg")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://126791609773.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-2:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}
	    
  }
}
