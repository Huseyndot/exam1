pipeline {
    agent any
    triggers {
      pollSCM '* * * * *'
        }
    stages {
        stage('Hello') {
            steps {
                echo "Hello World 1"
            }
        }
        stage('Build') {
            steps {
                echo "__Build and push dockerhub__"
                sh "docker build -t huseyn111/simple_python:v$BUILD_ID ."
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                sh "docker login -u $user -p $pass"
                sh "docker push huseyn111/simple_python:v$BUILD_ID"
              }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy"
                sh "docker run -d --name flask-app-$BUILD_ID -p 80$BUILD_ID:8080 huseyn111/simple_python:v$BUILD_ID"
            }

    }
}

}
