pipeline{
    agent any
    environment{
    PATH="/opt/apache-maven-3.9.6/bin:$PATH"
    }
    stages{
        stage('git-clone'){
            agent {
                label 'master'
            }
            steps {
                git 'https://github.com/Ravimore001/project-1.git'
                stash 'code'
            }
        }
        stage('build'){
            agent {
                label 'agent-1'
            }
            steps{
                unstash 'code'
                sh 'mvn clean install'
            }
        }
         stage('email-notifi'){
            agent {
                label 'agent-1'
            }
            steps{
                mail bcc: '', body: 'test has completed...', cc: '', from: '', replyTo: '', subject: 'testing mail.....', to: 'creativedevops2023@gmail.com'
            }
        }
        stage('docker-build'){
            agent {
                label 'agent-1'
            }
            steps{
                sh 'docker build -t ravimore001/my-app:1.8 .'
               
            }
        }
        stage('push-img'){
            agent {
                label 'agent-1'
            }
            steps{
               withCredentials([string(credentialsId: 'docker-img', variable: 'image')]) {
               sh 'docker login -u ravimore001 -p ${image}'
                } 
               echo "image push successfully" 
               
            }
        }
    }
}
