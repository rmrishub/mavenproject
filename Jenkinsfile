pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/rmrishub/mavenproject.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Maven project...'
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests...'
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging into JAR...'
                bat 'mvn package -DskipTests'
            }
        }

        stage('Run') {
            steps {
                echo 'Running the JAR file...'
                bat 'java -cp target/mavenproject-1.0-SNAPSHOT.jar com.example.AddNumbers'
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
