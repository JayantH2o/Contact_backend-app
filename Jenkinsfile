pipeline {
//    agent any
    agent {label 'slave-1'}
    tools {
      maven 'Maven-3.9.1'
            }
    stages {
        stage('git-clone') {
            steps {
                git branch: 'main', credentialsId: 'Git_credentials', url: 'https://github.com/JayantH2o/contact_backend-app.git'
            }
        }
        stage ('Maven Clean Build'){
            steps {
                sh 'mvn clean package'
                    }    
        
            }
    
        stage ('Build and push docker image'){
            steps{
                withCredentials([string(credentialsId: 'dockerAcntpwd', variable: 'dockerAcntpwd')]) {
                sh 'docker login -u jayachandrant -p ${dockerAcntpwd} '
                sh 'docker build -t jayachandrant/contact_backend_app .'
				sh 'docker push jayachandrant/contact_backend_app'
            }
        }   
        }
      /*  stage ('Deploy'){
            steps{
                sh 'kubectl apply -f Deployment.yml'
                sh 'kubectl get all -o wide'
               }
        }   */
        
    }
}

