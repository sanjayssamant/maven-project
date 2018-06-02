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
        stage ('Deploy To Production') {
            steps{
                timeout(time=5,unit='DAYS'){
                    input message: 'Approve Production Deployment'
                }
                build job: 'deploy-to-prod'
            }
            post {
                success{
                    echo 'Code deployed to Production'
                }
                failure{
                    echo 'Deployement failed.'
                }
            }
        }

    }
}