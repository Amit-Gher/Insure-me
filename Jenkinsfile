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
        
              
    }
}
