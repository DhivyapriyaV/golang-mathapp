pipeline {
    agent {label 'docker-agent'} 

    environment {
        imageName = "mygolangmathapp"
        dockerImage = ''
    }

    stages {
        stage('checkout scm') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/PriyaSIVATH/golang-mathapp.git']])
            }
        }

        stage('image build') {
            steps {
                script {
                    // echo "build"
                    dockerImage = docker.build imageName
                }
            }

        }



    }

}