pipeline{
    agent any

    tools {
         maven 'mvn'
         jdk 'java'
    }

    stages{
        stage('Initialize'){
            def dockerHome = '/Applications/Docker.app/Contents/Resources'
            #def mavenHome  = tool 'MyMaven'
            #env.PATH = "${dockerHome}/bin:${mavenHome}/bin:${env.PATH}"
            env.PATH = "${dockerHome}/bin:${env.PATH}"
        }
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/juan-solo/demo-java.git']]])
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
