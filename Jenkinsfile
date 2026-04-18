pipeline {
    agent {
        label 'built-in'
    }

    tools {
        maven 'Maven-3'
    }

    stages {

        stage('checkout code') {
            steps {
                git 'https://github.com/ShreehariBandrawad/myapp-project.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('save Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Setup DB') {
            steps {
                sh '''
                chmod +x setup-db.sh
                ./setup-db.sh
                '''
            }
        }

        stage('Deploy to slave') {
            steps {
                sh '''
                scp target/*.war root@172.31.17.227:/mnt/servers/apache-tomcat-10.1.54/webapps
                '''
            }
        }
    }
}
	
