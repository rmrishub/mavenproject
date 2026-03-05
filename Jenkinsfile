pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/rmrishub/mavenproject.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Maven project...'
                sh 'mvn clean compile'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging into JAR...'
                sh 'mvn package -DskipTests'
            }
        }

        stage('Run') {
            steps {
                echo 'Running the JAR file...'
                sh 'java -cp target/mavenproject-1.0-SNAPSHOT.jar com.example.AddNumbers'
            }
        }

        stage('Result') {
            steps {
                echo 'Maven project executed successfully!'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Maven Build and Run successful!'
        }
        failure {
            echo '❌ Something went wrong — check console output'
        }
    }
}