pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build First') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test Second') {
            steps {
                sh 'whereis mvn'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver Third') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
     }
} 
