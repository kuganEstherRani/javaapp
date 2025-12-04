pipeline {
    agent {
        docker{
            image 'nginx:1-alpine'
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
                sh 'docker --version'
                
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
