pipeline {
 agent any
 tools{ jdk 'JDK22'  }
 environment { 
JAVA_HOME = '/opt/homebrew/Cellar/openjdk/22.0.1/libexec/openjdk.jdk/Contents/Home'
DOCKER_TAG = getVersion()
 }
 stages {
 
 stage ('Clone Stage') {
 steps {
 git 'https://github.com/yesserabbes/CiCD.git'
 }
 }
 stage ('Docker Build') {
 steps {
 sh 'docker build -t yesserabbes/build:${DOCKER_TAG}.'
 }
 } 
stage ('DockerHub Push') {
steps {
 withCredentials([string(credentialsId: 'b10a942d-7af5-437c-a85a-74bff768d123', variable: 
'DockerHubPassword')]) {
 sh 'sudo docker login -u yesserabbes -p ${DockerHubPassword}'
 }
 sh 'sudo docker push yesserabbes/build:${DOCKER_TAG}'
 } } 

 } }
def getVersion(){
 def version = sh returnStdout: true, script: 'git rev-parse --short HEAD'
 return version
}