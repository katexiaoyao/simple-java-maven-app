pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v $HOME/.m2:/root/.m2'
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
                sh 'mvn -h'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Test Jmeter') {
            agent {
                image 'justb4/jmeter'
            }
            steps {
                sh 'jmeter -version'
            }
        
        }
        stage('Deliver Third') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
     }
} 
