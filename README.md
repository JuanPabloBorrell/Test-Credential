# pipeline {
    agent any
    stages{
        stage("demo"){
            steps{
                withCredentials([[
                    $class:'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'terraform-jenkins',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                        
                        sh "aws ec2 describe-instances --region=eu-central-1"
                }
            }
        }
    }
}