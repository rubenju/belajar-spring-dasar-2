pipeline {
    agent {
        node {
            label "linux && centos"
        }
    }
    stages {
        stage("Build") {
            steps {
                echo "Start build"
                sh("./mvnw clean compile test-compile")
                echo "Finished build"
            }
        }
        stage("Test") {
            steps {
                echo "Check docker container status"
                sh("sudo docker ps")
                echo "Check container status finished"
            }
        }
        stage("Deploy") {
            steps {
                echo "Hello Deploy 1"
                echo "Hello Deploy 2"
                echo "Hello Deploy 3"
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