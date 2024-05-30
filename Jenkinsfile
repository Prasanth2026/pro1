pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/Prasanth2026/pro1/', branch: "master"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t basitti/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push basitti/staragileprojectfinance:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name Me-first-containe2211 -p 8081:80 basitti/staragileprojectfinance:v1'
                    
                    }
                
            
        }
    }
}
