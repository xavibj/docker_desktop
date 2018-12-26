pipeline {
   agent any
   stages{
      stage('checkout'){
         steps{
            checkout scm
         }
      }
      stage('Build Atom Image') {
            when {
                changeset "atom/*"
            }
            steps {
                echo 'Building atom image, please wait ...'

                script {
                    withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
                       def customImage = docker.build("xavibj/atom:${env.BUILD_ID}","-f atom/Dockerfile .")
                       def latest = docker.build("xavibj/atom:latest","-f atom/Dockerfile .")
                       customImage.push()
                       latest.push()
                    }
                }
            }
       }
      stage('Build Tor-browser Image') {
            when {
                changeset "tor-browser/*"
            }
            steps {
                echo 'Building tor-browser image, please wait ...'

                script {
                    withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
                       def customImage = docker.build("xavibj/tor-browser:${env.BUILD_ID}","-f tor-browser/Dockerfile .")
                       def latest = docker.build("xavibj/tor-browser:latest","-f tor-browser/Dockerfile .")
                       customImage.push()
                       latest.push()
                    }
                }
            }
       }
   }
}
