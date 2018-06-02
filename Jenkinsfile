pipeline {
    agent any
    tools {
        maven "LocalMaven"
    }
    stages{
        stage('Build'){
            steps {
               bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }

        }
        stage ('Deploy To Staging') {
            steps {
                build job: 'deploy-to-staging'
            }

        }

    }
}