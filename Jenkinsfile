pipeline{
agent any
	stages{
		stage("checkout code") {
			steps{
			   checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub_Password', url: 'https://github.com/gosalapradeep/Kubernetes_Cluster.git']]])
			}
		}
		stage("Build the Image") {
			steps{
			  sh "docker build -t gosalapradeep/reactapp:$BUILD_NUMBER /home/ubuntu/Kubernetes_Cluster"
			}
		}
		stage("Push the code") {
			steps{
			  withCredentials([usernamePassword(credentialsId: 'DockerPass', passwordVariable: 'DockerHubPassword', usernameVariable: 'gosalapradeep')]) {
				  sh "docker login -u gosalapradeep -p ${DockerHubPassword}"
			  }
				sh "docker push gosalapradeep/reactapp:$BUILD_NUMBER"
			}
		}
	}
}
