pipeline {
    agent none
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    stages {
        stage('COMPILE') { 
            agent any   
            steps {
                    echo "COMPILING THE CODE"
                    sh 'mvn compile'
                  }
            }
        stage('UNITTEST'){
            agent any
        
            steps {
                    echo "RUNNING THE UNIT TEST CASES AND GENERATING REPORTS"
                    sh 'mvn test'
                  }
                post {
                    always {
                        junit 'target/surefire-reports/*.xml'
                    }
                }
            }
        stage('PACKAGE'){
        
            agent any
        
               steps{
               
                 sshagent(['build_server_key'])

                    echo "PACKAGING THE CODE"
                    //  sh 'mvn package'
                    sh "scp -o strictHostkeyChecking=no server-script.sh ec2-user@172.31.29.4:/home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no server-script.sh ec2-user@172.31.29.4 bash ~ec2-user/server-script.sh"
                    //  sh   "ssh ec2-user@ec2-54-234-105-122 sudo docker build -t /home/ec2-user/addressbook"
                    }
                }
        }
    }
