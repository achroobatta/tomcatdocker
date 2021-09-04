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
                sh "pwd"
                sh "ls -lrt"
                sh "echo ${env.BUILD_ID}"
                sh "docker build . -t tomcatdockerwebapp:${env.BUILD_ID}"                
            }
            
        }
        stage('Run container in environment'){
            steps{
                 sh "docker run -d -p 8090:8080 tomcatdockerwebapp:${env.BUILD_ID}"
            }
        }
    }
}