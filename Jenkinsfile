pipeline {
    agent any    
    options {
        disableConcurrentBuilds()
    }
    stages {
        stage ("checkout from GIT") {
            steps {
                sh 'git --version'
            }
        }
        stage ("terraform init") {
            steps {
                sh 'terraform init'
            }
        }    
        stage ("terraform validate") {
            steps {
                sh 'terraform validate'
            }
        }
        stage ("terrafrom plan") {
            steps {
                sh 'terraform plan '
            }
        }
        stage ("terraform apply") {
            steps {
                sh 'terraform apply --auto-approve'
            }
        }
    }
}
