pipeline {
    agent docker-agent

    stages {
        stage('checkout scm') {
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/PriyaSIVATH/golang-mathapp.git']])
        }



    }

}