pipeline {
    agent none
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
     environment{
        IMAGE_NAME='devopstrainer/java-mvn-privaterepos:$BUILD_NUMBER'
        DEV_SERVER_IP='ec2-user@52.66.240.173'
        APP_NAME='java-mvn-app'
    }
    stages {
        stage('COMPILE') {
            agent any
            tools{
        jdk 'myjava'
        mvn'mymaven'
    }
            steps {
                script{
                    echo "COMPILING THE CODE"
                    git 'https://github.com/preethid/addressbook.git'
                    tool name: 'mymaven', type: 'mvn'
                    
                    sh 'mvn compile'
                }
                          }
            }
        stage('UNITTEST'){
            agent any
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
        stage('PACKAGE+BUILD DOCKER IMAGE ON BUILD SERVER'){
            agent any
           steps{
            script{
            sshagent(['DEV_SERVER_KEY']) {
        withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                     echo "PACKAGING THE CODE"
                     sh 'package'
                    }
                    }
                }
            }
        }
