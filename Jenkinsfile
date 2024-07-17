pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/vidalgithub/jenkins-vault-demo.git'
            }
        }


        stage('Docker Demo') {
            steps {
                    withVault(configuration: [disableChildPoliciesOverride: false, timeout: 60, vaultCredentialId: 'vaultCred', vaultUrl: 'http://52.87.227.35:8200'], vaultSecrets: [[path: 'dockerhub/creds', secretValues: [[vaultKey: 'username'], [vaultKey: 'password']]]])  {
                        sh 'docker login -u $username -p $password'
                        sh 'docker build -t kemgou .'
                        sh 'docker tag kemgou vidaldocker/kemgou:demo'
                        sh 'docker push vidaldocker/kemgou:demo'
                    }
            }
        } 
    }
}
