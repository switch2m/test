pipeline {
    agent any
    stages {
        stage('npm install') {
            steps {
                echo 'installing packages'
                sh 'npm install'
            }
        }
        stage('build image') {
            steps {
                echo 'Building the image'
                withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t switch2mdock/delivmed:1.0 .'
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push switch2mdock/delivmed:1.0'
                }
            }
        }
        stage('build') {
            steps {
                echo 'Building the project'
                sh 'npm run build'
            }
        }
    }
}