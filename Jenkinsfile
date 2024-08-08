pipeline{
	agent any
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
						sh 'docker buildx build -t assesimage2:13 . '
																
}
}
}
			stage ('push image'){
			 steps{
			 	script{
				 withDockerRegistry(credentialsId: 'dtoken', url: 'https://hub.docker.com/repository/docker/kirti2024/assessmentpurpose/') {
					 sh 'docker tag assesimage2:13 kirti2024/assessmentpurpose:13'
					 sh 'docker push kirti2024/assessmentpurpose:13'
    
}
				}
			 }
			}
}
}
