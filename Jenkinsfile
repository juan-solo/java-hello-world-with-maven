pipeline{
    agent any

    tools {
         maven 'mvn'
         jdk 'java'
    }

    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/juan-solo/java-hello-world-with-maven.git']]])
            }
        }
        stage('build'){
            steps{
               sh 'mvn clean install'
            }
        }
        stage('cp-artifact'){
            steps{
                sh 'mkdir pkg'
                sh 'cp target/*.war pkg/'
            }
        }
        stage('build-deploy'){
            steps{
                sh 'docker build -t javademo:latest .'
                sh 'docker run -d -p 8081:8080 javademo:latest'
            }
        }

    
    }
    post{
        always{
            cleanWs()
        }
    }
}
