pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Test') {
            options {
                timestamps()
            }
            steps {
                sh "mvn test"
                sh "mvn --version"
                echo 'Testing Code'
                echo "Testing Done"
            }
        }
        stage('Build') {
            options {
                timestamps()
            }
            steps {
                sh "mvn package"
                echo 'Making Build'
                echo "Build Prepared"
            }
        }
        stage('Deploy In Test') {
            options {
                timestamps()
            }
            steps {
                // deploye on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'Tomcat Admin', path: '', url: 'http://localhost:8090')], contextPath: '/pipeline-app', war: '**/*.war'
                echo 'Deploying In Test'
                echo "Test Deployment Completed"
            }
        }
        stage('Deploy In Prod') {
            options {
                timestamps()
            }
            steps {
                // deploye on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'Tomcat Admin', path: '', url: 'http://localhost:8090')], contextPath: '/pipeline-prod-app', war: '**/*.war'
                echo 'Deploying In Prod'
                echo "Prod Deployment Completed"
            }
        }
    }
    post{
        always {
            echo "Running Post Actions Always"
        }
        success {
            echo "Running Post Actions On Success"
        }
        failure {
            echo "Running Post Actions On Failure"
        }
    }
}
