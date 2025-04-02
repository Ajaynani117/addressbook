pipeline {
    agent any
    stages {
        stage('COMPILE') {    
            steps {
                    echo "COMPILING THE CODE"
                    sh 'mvn compile'
                  }
            }
        stage('UNITTEST'){
            steps {
                    echo "RUNNING THE UNIT TEST CASES"
                    sh 'mvn test'
                  }
                post {
                    always {
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
