pipeline {
    agent any
    
    environment {
        TEST_SERVER = 'test-server'
        GIT_REPO = 'https://github.com/patilprem21/EDUREKA-DevOps-Projectcerti.git'
        DOCKER_IMAGE = 'devopsedu/webapp'
    }
    
    stages {
        stage('Job 1: Install Puppet Agent') {
            steps {
                script {
                    echo 'Installing Puppet Agent on slave node...'
                    sh '''
                        # Install Puppet agent directly on test-server
                        docker exec test-server apt-get update
                        docker exec test-server apt-get install -y puppet-agent
                        echo "Puppet Agent installation completed"
                    '''
                }
            }
        }
        
        stage('Job 2: Install Docker via Ansible') {
            steps {
                script {
                    echo 'Installing Docker on test server using Ansible...'
                    sh '''
                        # Use absolute path to ansible folder
                        cd ${WORKSPACE}/ansible
                        ansible-playbook -i inventory install-docker.yml
                    '''
                }
            }
        }
        
        stage('Job 3: Deploy PHP Application') {
            steps {
                script {
                    echo 'Pulling PHP application and deploying Docker container...'
                    sh '''
                        # Clone the repository
                        git clone ${GIT_REPO} php-app
                        cd php-app
                        
                        # Build and deploy Docker container
                        docker build -t ${DOCKER_IMAGE} .
                        docker run -d -p 8081:80 --name php-app-container ${DOCKER_IMAGE}
                        
                        # Check if container is running
                        docker ps | grep php-app-container
                        
                        echo "PHP application deployed successfully!"
                    '''
                }
            }
            post {
                failure {
                    script {
                        echo 'Job 3 failed. Cleaning up running container...'
                        sh '''
                            docker stop php-app-container || true
                            docker rm php-app-container || true
                            echo "Cleanup completed"
                        '''
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline completed!'
        }
        failure {
            script {
                echo 'Pipeline failed. Performing cleanup...'
                sh '''
                    docker stop php-app-container || true
                    docker rm php-app-container || true
                    echo "Final cleanup completed"
                '''
            }
        }
    }
}
