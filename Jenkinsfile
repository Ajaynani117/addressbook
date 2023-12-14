pipeline {
    agent any
    stages {
        stage('Compile') {
            steps {
                echo 'build the code '
                sh 'mvn compile'
            }
        }
        stage('Test') {
          steps {
            echo 'test the code '
            sh 'mvn test'
          }
        }
        stage('Package'){
            steps {
                echo 'package the code'
              sh  'mvn package'
            }
        }
    }
}
