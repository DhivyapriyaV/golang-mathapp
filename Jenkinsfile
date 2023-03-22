pipeline {
    agent {label 'docker-agent'} 

    environment {
        imageName = "mygolangmathapp"
        tagName = "v1.0.0"
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
                     dockerImage.push('latest')
                    //  dockerImage.push(tagName)
                     }

                    // This step should not normally be used in your script. Consult the inline help for details.
                    // withDockerRegistry(credentialsId: 'nexus-repo-manager', url: 'http://192.168.0.155:8085/') {
                    // dockerImage.push('v1.0.0')
                    // // some block
                    // }
                }
            }
        }

        // Stopping previous running Docker containers for cleaner Docker run 
        stage('stopping running containers') {
            steps {
                sh 'docker ps -f name=mygolangcontainer -q | xargs --no-run-if-empty docker container stop'
                sh 'docker container ls -a -fname=mygolangcontainer -q | xargs -r docker container rm'
            }
        }

        stage('docker run') {
            steps {
                script {
                    sh 'docker run -d -p 8010:8010 --rm --name mygolangcontainer ' + registry + imageName       // + tagName
                }
            }
        }



    }

}