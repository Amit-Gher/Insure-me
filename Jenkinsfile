pipeline {
    agent any
    tools {
      maven 'M2_HOME'
          }
    stages {
        stage('Git Checkout'){
            steps {
              git 'https://github.com/Amit-Gher/Insure-me.git'
            }
        }    
        stage('Build Package') {
            steps {
                sh 'mvn package'
            }    
        }  
         stage('Publish HTML Reports') {
            steps {
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Insure-me project/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
            }    
        }  
        stage('Create Docker Image') {
            steps {
                sh 'docker build -t amitg01/insure-me .'
            }    
        }  
        stage('Docker Image Push') {
            steps {
                
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u amitg01 -p ${dockerhubpwd}'
                    }    
                    sh 'docker push amitg01/insure-me'  
           }     
        }
         stage('Deploy Container') {
            steps {
                ansiblePlaybook credentialsId: 'SSH-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'prod.inv', playbook: 'deploy.yml'
            }    
        }  
}
}
    
