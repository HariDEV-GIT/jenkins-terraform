pipeline {
    agent any
    parameters {
        choice(name: 'ENVIRONNMENT', choices: ['dev', 'sit', 'prd'], description: 'Source brnach')
        string(name: 'FEATURE_BRANCH', defaultValue: '', description: 'Provide your feature branch name for downgrade')
        string(name: 'REVISES_ID', defaultValue: '', description: 'Revises ID for downgrade')
        file(name:'secret_file', description:'contains list secret file credential')
    }    
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
        /*stage ("terraform format check") {
            steps {
                sh('''
                    terraform fmt
                    git status
                    echo $BRANCH_NAME
                    git checkout $BRANCH_NAME
                    git add *.tf
                    git commit -am "Terraform fmt by Jenkins"
                    git status
                    git config --local user.name "jenkins local user"
                    git push origin $BRANCH_NAME
                ''')
            }
        }*/  
        stage ("terraform init") {
            stage ("testing") {
                stages ("dev") {
                    stage ("down") {
                       steps {
                          sh 'terraform init'
                       }
                    }    
                }
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
