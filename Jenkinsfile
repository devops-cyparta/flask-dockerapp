pipeline {
    agent {
        label 'agent1'
    }
    stages {
        stage ('Build') {
            steps {
                /*git branch: 'main', credentialsId: 'github_credential', url: 'https://github.com/devops-cyparta/flask_dockerApp.git' //not needed in jenkins in github but mandatory in jenkins pipeline */
                sh "docker build -t devopscyparta/jenkins-slave:${env.BUILD_NUMBER} ."
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass_dockhub', usernameVariable: 'user_dockhub')]) {
                     sh "docker login -u ${user_dockhub} -p ${pass_dockhub}"
                     sh "docker push devopscyparta/jenkins-slave:${BUILD_NUMBER}"
                }
            }
        }
        stage ('Deploy') {
            steps {
                sh "docker run -d -p 500${env.BUILD_NUMBER}:8080 devopscyparta/jenkins-slave:${env.BUILD_NUMBER}"
            }
        }
    }
}
