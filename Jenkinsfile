pipeline {
    agent any

    environment {
        TOMCAT_USER = credentials('TCadmin')  // Ensure this credential ID is correct
        TOMCAT_PASSWORD = credentials('admin')  // Ensure this credential ID is correct
        TOMCAT_URL = 'http://13.201.98.100:8090/manager/text/deploy?path=/'
    }

    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/LOHITHHJ07/simple-helloWorld-java-war_file.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deployment') {
            steps {
                script {
                    def warFile = sh(script: 'find target -name "*.war"', returnStdout: true).trim()
                    
                    sh """
                        curl -u ${TOMCAT_USER}:${TOMCAT_PASSWORD} \
                             -T ${warFile} \
                             ${TOMCAT_URL}
                    """
                }
            }
        }
    }
}



