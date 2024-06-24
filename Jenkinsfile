pipeline{
    agent any
    triggers{
        pollSCM('* * * * *')
    }
    stages {
        stage('git'){
            steps{
                git url: 'https://github.com/WorkshopsByKhaja/Terraform-June24.git',
                branch: 'develop'
            }
        }
        stage('build docker image'){
            steps{
                sh 'docker image build -t kumar1502/nop-demo-terraform:latest .'
                sh 'docker image push kumar1502/nop-demo-terraform:latest'
            }
        }
        stage('infra provisioning'){
            steps{
                sh 'cd infra/terraform && terraform init && terraform workspace selecct dev && pwd && terraform apply -var-file="dev.tfvars" -var"build_number=${BUILD_ID}" -auto-approve'

            }
        }
        stage('deploy'){
            steps{
                sh 'kubectl apply -f infra/k8s'
            }
        }
    




}
