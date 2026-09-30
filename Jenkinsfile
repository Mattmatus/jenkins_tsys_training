pipeline {
 environment {
 imagename = "matthew25130607/jenkins-tsys" // change the image
 image_tag    = "${BUILD_NUMBER}" // Sets version to current Jenkins build number
 registryCredential = 'matthew25130607' // docker credentails
 dockerImage = ''
 }
 agent any
 stages {
 stage('Cloning Git') {
 steps {
 git([url: 'https://github.com/Mattmatus/jenkins_tsys_training.git', branch: 'main']) // change the git url
 }
 }
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build imagename
 }
 }
 }
 stage('Running image') {
 steps{
 script {
 sh "docker run -itd -P ${imagename}:latest"
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
