pipeline {
    agent any
    stages {
        stage('COMPILE') {
            agent any
            
            steps {
                script{
                    echo "COMPILING THE CODE"
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
        stage('PACKAGE'){
            agent any
           steps{
                echo "PACKAGING THE CODE"
                     sh 'package'
                    }
                    }
                }
       }
