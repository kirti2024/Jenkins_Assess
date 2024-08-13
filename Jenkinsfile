pipeline{
	agent any
	environment{
	DOCKER_PASSWORD="dtoken"
		AWS_CRED = "awscred"
KUBECONFIG_FILE = "/tmp/kubeconfig"

		
}
		stages{
			stage('Checkout'){
				steps{
					script{
   checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kirti2024/Jenkins_Assess.git']])
}
				}
			}
			stage('build image'){
				steps{
					script{
						sh 'docker buildx build -t assesimage2:15 .'
						
						sh 'docker tag assesimage2:15 kirti2024/assessmentpurpose:15'
						
																
}
}
}
	stage ('push image'){
		steps{
			 script{
				 withCredentials([usernamePassword(credentialsId: "${DOCKER_PASSWORD}", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push kirti2024/assessmentpurpose:15
                        """
            }

 
			 }
			}
}



stage('Deploy to K8s'){
              steps{
		script{ 
		withAWS(credentials:AWS_CRED, region: 'us-east-1'){
sh """aws eks update-kubeconfig --name AssessCluster --kubeconfig $KUBECONFIG_FILE  """
}
withENV(["KUBECONFIG=${KUBECONFIG_FILE}"]){
 sh """ kubectl apply -f  deployment.yaml """
}
}
}
	      }

			
}
}
