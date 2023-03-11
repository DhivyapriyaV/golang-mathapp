pipeline {
    agent {label 'docker-agent'} 

    stages {
        stage('checkout scm') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/PriyaSIVATH/golang-mathapp.git']])
            }
        }



    }

}