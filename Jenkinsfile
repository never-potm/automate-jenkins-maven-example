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
            // We need to trigger Deploy_Application_Staging_Env job
            build job: 'Deploy_Application_Staging_Env'
        }
    }
}