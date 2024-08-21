pipeline {
    
    agent {
        docker {
            image 'docker:latest' // The base image for building the Docker image
            // args '-v /var/run/docker.sock:/var/run/docker.sock' // Bind Docker socket for building
            args '--network=jenkins_gsis_jenkins_network -e DOCKER_HOST=tcp://docker-proxy:2375'
            reuseNode true // Allows reusing the agent for the entire pipeline
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
                    docker build -t test_mpla_kostaras_new ./mpla/
                '''
                // dir('mpla') {
                //     // Build the Docker image using the Dockerfile in the repository
                //     sh 'ls -alh'
                //     sh 'pwd'
                //     echo "$DOCKER_HOST"
                //     sh 'docker ps'
                //     sh 'docker build -t test_mpla_kostaras .'
                // }
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
