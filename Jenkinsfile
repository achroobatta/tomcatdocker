pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Create docker build'){
            steps{
                sh 'docker build . -t tomcatdockerwebapp:${env.BUILD_ID}'

            }
            
        }
        stage('Run container in environment'){
            steps{
                 sh 'docker run tomcatdockerwebapp:${env.BUILD_ID} -p 8090:8080'
            }
        }
    }
}