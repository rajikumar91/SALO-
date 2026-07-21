pipeline {
    agent any

    tools {
        jdk 'Java21'
        maven 'Maven3'
    }

    parameters {
        string(name: 'ECR_REPO_NAME', defaultValue: 'amazon-prime', description: 'Enter repository name')
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=SALO \
                        -Dsonar.projectName="SALO Project" \
                        -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }

        /*stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: false
                }
            }
    }
*/
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${params.ECR_REPO_NAME} ."
            }
        }
    }
}
