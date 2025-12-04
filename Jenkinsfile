pipeline {
    agent {
        docker{
            image 'maven:3.8.6-openjdk-17'
        }
    }

   

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/kuganEstherRani/javaapp.git',
                        credentialsId: 'jenkins_github'
                    ]]
                ])
            }
           
        }

        stage('Build') {
            steps {
               
                sh 'mvn clean compile'
            }
        }

       
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
       
       

          
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
