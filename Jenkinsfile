pipeline {
    agent any

    environment {
        IMAGE_NAME='ajaynani117/test:$BUILD_NUMBER'
        BUILD_SERVER_IP='ec2-user@172.31.84.2'
    }
    stages {
        stage('COMPILE') {
            
            steps {
                script{
                    echo "COMPILING THE CODE"
                    sh 'mvn compile'
                }
                          }
            }
        stage('UNITTEST'){
            steps {
                script{
                    echo "RUNNING THE UNIT TEST CASES"
                    sh 'mvn test'
                }
             
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'
                }
            }
            }
        stage('PACKAGE'){
         agent any 
           steps{
                 sshagent(['build-server-key']) {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {

                   echo "Package the code"
                     //sh 'mvn package'
                     sh "scp -o StrictHostKeyChecking=no server-script.sh ${BUILD_SERVER_IP}:/home/ec2-user"
                     sh "ssh -o StrictHostKeyChecking=no ${BUILD_SERVER_IP} bash ~ec2-user/server-script.sh"
                     sh "ssh  ${BUILD_SERVER_IP} sudo docker build -t ${IMAGE_NAME} /home/ec2-user/addressbook"
                     sh "ssh  ${BUILD_SERVER_IP} sudo docker login -u $USERNAME -p $PASSWORD"
                     sh "ssh  ${BUILD_SERVER_IP} sudo docker push ${IMAGE_NAME}"
                     }
                
                    }
                    }
                }
       }
}