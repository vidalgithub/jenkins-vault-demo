pipeline {

    agent any
  
    stages{
         
        stage('Git Checkout'){
            //when { expression {  params.action == 'create' } }
            steps{
            gitCheckout(
                branch: "main",
                url: "https://github.com/vikash-kumar01/mrdevops_java_app.git"
            )
            }
        }

        stage('Docker Image Build : ECR'){
            //when { expression {  params.action == 'create' } }
             steps{
                withVault(configuration: [disableChildPoliciesOverride: false, timeout: 60, vaultCredentialId: 'vaultCred', vaultUrl: 'http://172.25.11.223:8200'], vaultSecrets: [[path: 'dockerhub/creds', secretValues: [[vaultKey: 'username'], [vaultKey: 'password']]]]) {
                  sh 'docker login -u $username -p $password'
                  sh 'docker build -t kemgou .'
                  sh 'docker tag kemgou vidaldocker/kemgou:demo'
                  sh 'docker push vidaldocker/kemgou:demo'
                }
            }
        }
    } // end of stages
} // end of pipeline

