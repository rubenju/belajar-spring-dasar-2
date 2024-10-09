pipeline {
    // agent {
    //     node {
    //         label "linux && centos"
    //     }
    // }
    agent none
    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }
    stages {
        stage("Prepare") {
            environment {
                APP = credentials("ben_rahasia")
            }
            agent {
                node {
                    label "linux && centos"
                }
            }
            steps {
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("App User : ${APP_USR}")
                sh('echo "App Password : $APP_PSW" > "rahasia.txt"')
            }
        }
        stage("Build") {
            agent {
                node {
                    label "linux && centos"
                }
            }
            steps {
                script {
                    def data = [
                        "firstName" : "Ben",
                        "lastName" : "Ju"
                    ]
                    writeJSON(file: "data.json", json:data)
                }
                echo "Start build"
                sh("./mvnw clean compile test-compile")
                echo "Finished build"
            }
        }
        stage("Test") {
            steps {
                echo "Check docker container status"
                // sh("sudo docker ps")
                echo "Check container status finished"
            }
        }
        stage("Deploy") {
            agent {
                node {
                    label "linux && centos"
                }
            }
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