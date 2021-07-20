pipeline{
    agent any
    tools {
        maven 'MAVEN'
    }
    stages {
        stage('Build Maven') {
            steps{
              checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/pidikiti1149/jenkins-docker-example.git']]])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
        }
        

         stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t pidikiti1149/my-app-1.0 .'
                }
            }
        }
        
           stage('Deploy Docker Image') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'pidikiti1149', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u pidikiti1149 -p ${dockerhubpwd}'
                 }  
                 sh 'docker push pidikiti1149/my-app-1.0:latest'
                }
            }
        }
        
    }
}
