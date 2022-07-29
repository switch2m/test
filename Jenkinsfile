def gv

pipeline {
    agent any
    stages {
        stage('init') {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage('npm install') {
            steps {
                script {
                    gv.package_install()
                }
            }
        }
        stage('build image') {
            steps {
                echo 'Building the image'
                withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t switch2mdock/test:2.0 .'
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push switch2mdock/test:2.0'
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