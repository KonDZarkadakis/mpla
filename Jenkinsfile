// currentBuild.displayName = "Docker-Agent#"+currentBuild.number

pipeline {
    
    agent {
        // label 'kostaras-agent'
        docker {
            image 'docker:latest' // The base image for building the Docker image
            args '--network=jenkins_gsis_jenkins_network -e DOCKER_HOST=tcp://docker-proxy:2375'
            reuseNode true
        }
    }

    // environment {
    //     DOCKER_HOST = 'tcp://docker-proxy:2375' // Set the Docker host environment variable for all stages
    // }

    stages {
        
        stage('Initialize') {
            steps {
                sh '''
                echo "====== Start of Environment Check ======"

                echo "Current User:"
                whoami

                echo "Current Hostname:"
                hostname

                echo "Current Working Directory:"
                pwd

                echo "Listing Files in Current Directory:"
                ls -alh
                
                ip addr
                echo "$DOCKER_HOST"
                docker ps

                echo "====== End of Environment Check ======"
                '''
            }
        }
        
        stage ('Repo pull') {
            steps {
                // Clone the repository
                sh 'git clone https://github.com/KonDZarkadakis/mpla.git'
            }
        }
        
        stage ('Build Image') {
            steps {
                sh '''
                    echo "$DOCKER_HOST"
                    docker ps
                    docker build --no-cache -t test_mpla_kostaras_new ./mpla/
                '''
            }
        }
        
        stage ('Finalize') {
            steps {
                sh '''
                pwd
                ls -alh
                '''
            }
        }
    }
    
    
    post {
        always {
            sh 'rm -rf mpla/'
        }
    }
    
    
}
