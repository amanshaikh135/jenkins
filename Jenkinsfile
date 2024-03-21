pipeline {
    agent any
    stages {
        stage('dev image build') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    def app = docker.build("shaikhamann/dev:latest")
                    docker.withRegistry('https://registry.hub.docker.com/shaikhamann/dev', 'dockerhub_creds') {
                        app.push()
                    }
                }
            }
        }
        stage('qa image build') {
            when {
                branch 'qa'
            }
            steps {
                script {
                    def app = docker.build("shaikhamann/qa:latest")
                    docker.withRegistry('https://registry.hub.docker.com/shaikhamann/qa', 'dockerhub_creds') {
                        app.push()
                    }
                }
            }
        }
    }

    post { 
        always { 
            echo 'Deleting Project now !! '
            deleteDir()
        }
    }
}
