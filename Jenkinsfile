pipeline {
    agent any
    options {
        disableConcurrentBuilds()
    }
    tools {
        terraform 'terraform'
    }
    stages {
        stage ("checkout from GIT") {
            steps {
                git branch: 'main', url: 'https://github.com/HariDEV-GIT/jenkins-terraform.git'
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
        stage ("terraform format check") {
            steps {
                sh('''
                    terraform fmt
                    git add .
                    git commit -m "Terraform fmt by Jenkins"
                    git push
                ''')
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