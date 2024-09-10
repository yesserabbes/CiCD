stage ('Clone Stage') {
 steps {
 git 'https://github.com/yesserabbes/CiCD.git'
 }
 }
environment {
 DOCKER_TAG = getVersion()
}

stage ('Docker Build') {
 steps {
 sh 'docker build -t yesserabbes/build:${DOCKER_TAG}.'
} }

stage ('DockerHub Push') {
steps {
 withCredentials([string(credentialsId: 
'b10a942d-7af5-437c-a85a-74bff768d123', variable: 
'DockerHubPassword')]) {
 sh 'sudo docker login -u yesserabbes -p ${DockerHubPassword}'
 }
 sh 'sudo docker push yesserabbes/build:${DOCKER_TAG}'
 } }
 steps{
sshagent(credentials: ['Vagrant_ssh']) {
 sh "ssh user@Ip_Recette"
 sh "ssh user@Ip_Recette ‘sudo docker run “image_name:${DOCKER_TAG}"’”
} 
} }

 def version = sh returnStdout: true, script: 'git rev-parse --short HEAD'
 return version
}
