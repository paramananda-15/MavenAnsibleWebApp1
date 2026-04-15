pipeline {
    agent any

    environment {
        LANG = 'C.UTF-8'
        LC_ALL = 'C.UTF-8'
    }

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/paramananda-15/MavenAnsibleWebApp1-CICD.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                export LANG=C.UTF-8
                export LC_ALL=C.UTF-8
                ansible-playbook ansible/playbook.yml -i ansible/hosts.ini
                '''
            }
        }
    }
}
