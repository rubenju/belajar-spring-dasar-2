pipeline {
    agent {
        node {
            label "linux && centos"
        }
    }
    stages {
        stage("Build") {
            steps {
                echo "Hello Build"
            }
        }
        stage("Test") {
            steps {
                echo "Hello Test"
                sh(error)
            }

        }
        stage("Deploy") {
            steps {
                echo "Hello Deploy"
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
