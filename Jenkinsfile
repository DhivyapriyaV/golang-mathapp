pipeline {
    agent {label 'docker-agent'} 

    environment {
        imageName = "mygolangmathapp"
        registryCredentials = "nexus-repo-manager"
        registry = "192.168.0.155:8085/"
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

        stage('nexus - upload image') {
            steps {
                script {
                    docker.withRegistry( 'http://'+registry, registryCredentials ) {
                     // dockerImage.push('latest')
                     dockerImage.push('v1.0.0')
                     }

                    // This step should not normally be used in your script. Consult the inline help for details.
                    // withDockerRegistry(credentialsId: 'nexus-repo-manager', url: 'http://192.168.0.155:8085/') {
                    // dockerImage.push('v1.0.0')
                    // // some block
                    // }
                }
            }
        }


    }

}