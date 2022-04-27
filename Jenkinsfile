node {
  
   stage("checkout code"){
       checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub_Password', url: 'https://github.com/gosalapradeep/Kubernetes_Cluster.git']]])
   }
   stage("Build Image"){
       sh "docker build -t gosalapradeep/reactapp:$BUILD_NUMBER /home/ubuntu/Kubernetes_Cluster"
   }
   stage("Push the Image"){
       withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) {
         sh "docker login -u gosalapradeep -p ${Docker_Hub_Password}" 
       }
       sh "docker push gosalapradeep/reactapp:$BUILD_NUMBER"
   }
}
