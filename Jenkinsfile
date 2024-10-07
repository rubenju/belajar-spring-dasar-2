pipeline {
    agent {
        node {
            label "linux && centos"
        }
    }
    stages {
        stage("Hello") {
            steps {
                echo "Hello World"
            }
        }
    }
    post {
        always {
            echo "I will always says hello again."
        }
        success {
            echo "Yes, success."
        }
        failure {
            echo "Oh no, failed."
        }
        cleanup {
            echo "Don't care success or error."
        }
    }
}