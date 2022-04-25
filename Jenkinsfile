pipeline {
    agent any
    

    stages {
        stage('SCM-checkout') {
            steps {

                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Ongraph-Pradeep/React_Docker']]])
            }
        }
	    stage('build image') {
		    steps {
				sh 'docker build -t gosalapradeep/reactapp:$BUILD_NUMBER /home/ubuntu/Kubernetes_Cluster';
		   }
		}
	     stage('Push Docker Image'){
                withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
                  sh "docker login -u dockerhandson -p ${Docker_Hub_Pwd}"
        }
                 sh 'docker push dockerhandson/java-web-app'
     }
    }
}
