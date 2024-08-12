pipeline{
	agent any
	environment{
	DOCKER_PASSWORD="dtoken"
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
		withKubeCredentials([credentialsId : 'kubesecret', serverUrl:'https://6DB421C38B80BEBC06436AF66D5A35B9.gr7.us-east-1.eks.amazonaws.com']){
sh """ kubectl apply -f  deployment.yaml"""

}
}
}
	      }

			
}
}
