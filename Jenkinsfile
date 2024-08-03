pipeline {
    agent any

    environment {
        // Define environment variables
        TOMCAT_USER = credentials('TCadmin')  // Fetch username from Jenkins credentials
        TOMCAT_PASSWORD = credentials('admin')  // Fetch password from Jenkins credentials
        TOMCAT_URL = 'http://13.201.98.100:8090/manager/text/deploy?path=/'
    }

    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/LOHITHHJ07/simple-helloWorld-java-war_file.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('DeploymentDev') {
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

    post {
        always {
            cleanWs()
        }
    }
}
