pipeline{
	agent any
	environment{
	DOCKER_PASSWORD=credentials('dtoken')
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
						sh 'docker buildx build -t assesimage2:13 .'
						sh 'docker tag assesimage2:13 kirti2024/assessmentpurpose:13'
						
																
}
}
}
			stage ('push image'){
			 steps{
			 	script{
				 withCredentials([string(credentialsId: 'dtoken', variable: 'DOCKER_PASSWORD')]) {
                sh """
                echo "$DOCKER_PASSWORD" | docker login -u kirti2024 --password-stdin https://index.docker.io/v1/
                docker push kirti2024/assessmentpurpose:13
                """
            }

 
			 }
			}
}
}
}
