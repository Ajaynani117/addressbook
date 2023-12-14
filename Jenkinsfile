pipeline {
    agent any
    stages {
       agent any 
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
           steps{
                echo "PACKAGING THE CODE"
                     sh 'mvn package'
                    }
                    }
                }
       }
