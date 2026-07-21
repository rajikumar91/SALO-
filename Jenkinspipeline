pipeline {
    agent any
    tools {
        jdk 'Java21'
        maven 'Maven3'
    }

    stages {
        stage('git-repo') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/rajikumar91/SALO-.git'
            }
        }

        stage('build maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('test maven') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
