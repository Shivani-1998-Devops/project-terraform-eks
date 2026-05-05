pipeline {
    agent any

    parameters {
        choice(
            name: 'ACTION',
            choices: ['apply', 'destroy'],
            description: 'Select the action to perform'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Shivani-1998-Devops/project-terraform-eks.git'
            }
        }
    
        stage ("terraform init") {
            steps {
                sh "terraform init -reconfigure"
            }
        }
        
        stage ("plan") {
            steps {
                sh "terraform plan"
            }
        }

        stage ("Action") {
            steps {
                script {
                    if (params.ACTION == 'apply') {
                        echo 'Executing Apply...'
                        sh "terraform apply --auto-approve"
                    } else if (params.ACTION == 'destroy') {
                        echo 'Executing Destroy...'
                        sh "terraform destroy --auto-approve"
                    } else {
                        error 'Unknown action'
                    }
                }
            }
        }
    }
}