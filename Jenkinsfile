pipeline {
environment {
imagename = "gosalapradeep/reactapp"
registryCredential = 'Docker_Password'
dockerImage = ''
}
agent any
stages {
stage('Cloning Git') {
steps {
git([url: 'https://github.com/gosalapradeep/Kubernetes_Cluster.git', branch: 'master', credentialsId: 'GitHub_Password'])
}
}
stage('Building image') {
steps{
script {
dockerImage = docker.build imagename
}
}
}
stage('Deploy Image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push("$BUILD_NUMBER")
dockerImage.push('latest')
}
}
}
}
}
}
