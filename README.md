# Rockpapergame
pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "ORACLEJDK17"
    }
    
    stages {
        stage ('fetch code'){
            steps {
                git branch: 'main', url: 'https://github.com/hkhcoder/vprofile-project.git'
            }
        }
        stage ('Build code'){
            steps{
                sh 'mvn install -DskipTest'
            }
            post{
                success {
                    echo 'Archievinig artifact'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        
        stage('Unit Test'){
            steps{
                sh 'mvn test'
            }
        }
    }







pipeline {
    agent any
    stages {
        stage ('fetch code'){
            steps {
                git branch: 'master', url: 'https://github.com/ajay-raut/nodeproject.git'
            }
        }
        stage ('Build code'){
            steps{
                sh 'sudo docker build -t nodejsapp .'
            }
        }
        
        stage('run container'){
            steps{
                sh 'sudo docker run -d -p 3000:3000 nodejsapp'
            }
        }
    }
}



}
