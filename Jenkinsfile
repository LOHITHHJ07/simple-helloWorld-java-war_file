pipeline {
    agent any

    environment {
        // Define environment variables if needed
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                git url: 'https://github.com/LOHITHHJ07/simple-helloWorld-java-war_file.git'
            }
        }

        stage('Build') {
            steps {
                // Build the project using Maven
                sh 'mvn clean install'
            }
        }
    }
}



