pipeline {
    agent any
    environment {
        MYSQL_ROOT_PASSWORD = credentials("MYSQL_ROOT_PASSWORD")
        DOCKER_USERNAME = "htrvolker"
        DOCKER_PASSWORD = credentials("DOCKER_PASSWORD")
        install_dependencies = "false"
    }
    stages {
        stage("Install Dependencies"){
            steps {
                script {
                    if (env.install_dependencies == 'true') {
                            sh "bash install-dependencies.sh"
                    }
                }
            }
        }
        stage("Docker Login") {
            steps {
                sh "echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin"
            }
        }
        stage("Build"){
            steps {
                sh "docker-compose build --parallel"
            }
        }
        stage("Push"){
            steps {
                sh "docker-compose push"
            }
        }
        stage("Deploy"){
            steps {
                sh "docker-compose up -d"
            }
        }
    }
}
