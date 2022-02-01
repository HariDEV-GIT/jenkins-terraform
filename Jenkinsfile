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
                    git add *.tf
                    git commit -m "Terraform fmt by Jenkins"
                    git config --global user.name "HariDEV-GIT"
                    git config --global user.email "harimadhan07@gmail.com"
                    git push origin main
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