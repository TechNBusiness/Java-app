pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("build jar") {
            steps {
                echo 'bulding the application...'
                sh 'mvn package'
                }
            }
            stage("build image") {
            steps {
                echo 'bulding the docker image...'
                withCredentials([usernamePassword(credentialsId: 'docker-hu-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t gazzytarget/my-repo:jma-2.0 .'
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push gazzytarget/my-repo:jma-2.0'
                }
                }
            }
        stage("test") {
            steps {
                    echo "testing the application..."
                }
            }
        stage("deploy") {
            steps {
                    echo 'deploying the application...'
                }
        }
    }
}
