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
			  withCredentials([usernameColonPassword(credentialsId: 'Docker_Hub_Password', variable: 'Docker_Hub_Password')]) {
				  sh "docker login -u gosalapradeep -p ${Docker_Hub_Password}"
			  }
				sh "docker push gosalapradeep/reactapp:$BUILD_NUMBER"
			}
		}
	}
}
