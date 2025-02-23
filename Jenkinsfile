pipeline {
    agent {
        label 'agent1'
    }
    stages {
        stage ('Build') {
            steps {
                sh "docker build -t test-jenkins-cont:${BUILD_NUMBER} ."
                
            }
        }
        stage ('Test') {
            steps {
                echo "Test Stage (Running)"
            }
        }
        stage ('Deploy') {
            steps {
                sh "docker run -d -p 200${BUILD_NUMBER}:8080 test-jenkins-cont:${BUILD_NUMBER}"
            }
        }
    }
}
