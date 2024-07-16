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
                    withVault(configuration: [timeout: 60, vaultCredentialId: 'vaultCred', vaultUrl: 'http://http://172.25.11.223:8200'], vaultSecrets: [[path: 'dockerhub/creds', secretValues: [[vaultKey: 'username'], [vaultKey: 'password']]]])  {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'docker build -t kemgou .'
                        sh 'docker tag kemgou vidaldocker/kemgou:demo'
                        sh 'docker push vidaldocker/kemgou:demo'
                    }
            }
        }
    }
}
