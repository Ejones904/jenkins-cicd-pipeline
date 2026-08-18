pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    stages {
                stage('build app') {
            steps {
                script {
                    echo 'building the application...'
                    sh 'mvn clean package'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh "docker build -t ejones904/demo-app:jma2.0 ."
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh "docker push ejones904/demo-app:jma2.0"
                    }
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo 'deploying docker image...'
                }
            }
        }
        
         }
        }
    
