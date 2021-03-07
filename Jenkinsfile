pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Now archiving the artifaccts..."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Deploy in Staging environment') {
            steps {
                build job: 'Deploy_Application_Staging_Env'
            }
        }
        stage('Deploy in Production environment') {
            steps {
                timeout(time:5, unit:'DAYS') {
                    input message:'Approve PRODUCTION deployment?'
                }
                build job: 'Deploy_Application_Prod_Env'
            }
        }
    }
}