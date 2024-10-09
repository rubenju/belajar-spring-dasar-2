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

    // triggers {
    //     cron("*/5 * * * *")
    // }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    stages {

        stage("OS Setup") {
            matrix {
                axes {
                    axis {
                        name "OS"
                        values "linux", "windows", "mac"
                    }
                    axis {
                        name "ARC"
                        values "32", "64"
                    }
                }
                stages {
                    stage("OS Setup") {
                        steps {
                            echo "Setup ${OS} ${ARC}"
                        }
                    }
                }
            }
        }

        stage("Preparation") {
            parallel {
                stage("Prepare Java") {
                    agent {
                        node {
                        label "linux && centos"
                        }
                    }
                    steps {
                        echo("Prepare Java")
                        sleep(5)
                    }
                }
                stage("Prepare Maven") {
                    agent {
                        node {
                        label "linux && centos"
                        }
                    }
                    steps {
                        echo("Prepare Maven")
                        sleep(5)
                    }
                }
            }
        }

        stage("Parameter") {
            steps {
                echo "Hello ${params.NAME}"
                echo "You description is ${params.DESCRIPTION}"
                echo "Your social media is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
            }
        }

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
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "osi"
            }
            steps {
                echo "Hello Deploy 1"
                echo "Hello Deploy 2"
                echo "Hello Deploy 3"
            }
        }

        stage("Release") {
            when {
                expression {
                    return params.DEPLOY
                }
            }
            steps {
                echo "Release it"
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