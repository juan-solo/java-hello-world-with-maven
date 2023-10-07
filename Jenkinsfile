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
               sh 'mvn package'
            }
        }
    }
    post{
        always{
            cleanWs()
        }
    }
}
