pipeline {
    agent any    
    options {
        disableConcurrentBuilds()
    }
    stages {
        stage ("git version") {
            steps {
                sh 'git --version'
            }
        }
        stage ("terraform version") {
            steps {
                sh 'terraform --version'
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
