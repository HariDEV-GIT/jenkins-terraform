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
        stage ("terraform format check") {
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'secrets', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRETS_ACCESS_KEY']]) {
                    sh('''
                        terraform fmt
                        git status
                        echo $BRANCH_NAME
                        git checkout $BRANCH_NAME
                        git add *.tf
                        git commit -am "Terraform fmt by Jenkins"
                        git status
                        git push https://${AWS_ACCESS_KEY_ID}:${AWS_SECRETS_ACCESS_KEY}@github.com/HariDEV-GIT/jenkins-terraform.git $BRANCH_NAME
                    ''')
                }   
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
