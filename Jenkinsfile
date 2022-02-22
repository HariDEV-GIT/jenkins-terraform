pipeline {
    agent any
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
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
        stage ("terraform format check") {
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
