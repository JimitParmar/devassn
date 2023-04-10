pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [],
                    submoduleCfg: [],
                    userRemoteConfigs: [[
                        url: 'https://github.com/JimitParmar/devassn'
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                withEnv(['TERM=dumb']) {
                    sh 'echo 123 | sudo -S npm install -g http-server'
                }
            }
        }
    }
}
