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
	    stage ('Push the image') {
		    steps {
		            sh 'docker push gosalapradeep/reactapp:$BUILD_NUMBER'
		    }
	    }
    }
}
