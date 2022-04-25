pipeline {
    agent any
    

    stages {
        stage('SCM-checkout') {
            steps {

                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'd4af5848-1f0e-4f40-a560-34ec92eeefff', url: 'https://github.com/gosalapradeep/Kubernetes_Cluster.git']]])
            }
        }
	    stage('build image') {
		    steps {
				sh 'docker build -t gosalapradeep/reactapp:$BUILD_NUMBER /home/ubuntu/Kubernetes_Cluster';
		   }
		}
	     stage('Push Docker Image'){
                withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
                  sh "docker login -u gosalapradeep -p ${Docker_Hub_Pwd}"
        }
                 sh 'docker push gosalapradeep/reactapp:$BUILD_NUMBER'
     }
    }
}
