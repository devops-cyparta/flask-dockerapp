pipeline {
    agent any
    stages {
        stage ('Build') {
            steps {
                /*git branch: 'main', credentialsId: 'github_credential', url: 'https://github.com/devops-cyparta/flask_dockerApp.git' //not needed in jenkins in github but mandatory in jenkins pipeline */
                sh "docker build -t devopscyparta/test-jenkins-cont:${env.BUILD_NUMBER} ."
                withCredentials([usernamePassword(credentialsId: 'dockerhub_credential', passwordVariable: 'PassDocker', usernameVariable: 'userDocker')]) {
                     sh "docker login -u ${userDocker} -p ${PassDocker}"
                     sh "docker push devopscyparta/test-jenkins-cont:${BUILD_NUMBER}"
                }
            }
        }
        stage ('Deploy') {
            steps {
                sh "docker run -d -p 500${env.BUILD_NUMBER}:8080 devopscyparta/test-jenkins-cont:${env.BUILD_NUMBER}"
            }
        }
    }
}
