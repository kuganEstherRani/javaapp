pipeline {
    agent any

    tools {
        maven 'Maven3'          // Name of Maven installation in Jenkins
        jdk   'JDK17'           // Name of JDK installed in Jenkins
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
                sh 'docker --version'
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

            stage('Deploy to Azure') {
            steps {
                withCredentials([string(credentialsId: 'clientId', variable: 'CLIENT_ID'), string(credentialsId: 'clientSecret', variable: 'CLIENT_SECRET'),string(credentialsId: 'TENANT_ID', variable: 'tenantid')]) {
               /* sh '''
                az login --service-principal -u $CLIENT_ID -p $CLIENT_SECRET --tenant $tenantid
                az webapp deploy --resource-group noteExpress_webapp --name javaappgithub --src-path target/*.jar --type jar
                 '''*/
                }
               
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
