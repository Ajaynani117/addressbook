pipeline {
    agent any
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
                   echo "Package the code"
                     //sh 'mvn package'
                     sh "scp -o StrictHostKeyChecking=no server-script.sh ec2-user@172.31.84.2:/home/ec2-user"
                     sh "ssh -o StrictHostKeyChecking=no server-script.sh ec2-user@172.31.84.2 ~/server-script.sh"
                     //sh "ssh  ec2-user@172.31.84.2 sudo docker build -t imagename /home/ec2-user/addressbook"
                     }
                
                    }
                    }
                }
       }
