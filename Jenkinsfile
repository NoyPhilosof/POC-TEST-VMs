properties([githubProjectProperty(displayName: '', projectUrlStr: 'https://github.com/NoyPhilosof/POC-TEST.git/')])

pipeline {
    agent { label 'ubuntu' }

    stages {
        
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'http://github.com/NoyPhilosof/POC-TEST.git'
            }
        }
        
        
        stage('Create SSH Key') {
            steps {
                catchError(message: 'Creating SSH key') {
                    script {
                        try{
                            sh '''ssh-keygen -f ~/.ssh/id_rsa -q -N ""
                            chmod 400 ~/.ssh/id_rsa'''
                        }                
                        catch (e) {
                            echo "default SSH Key exists"
                        }
                    }                
                }
            }
        }
        

        stage('Clean Old VMs') {
            steps {
                catchError(message: 'Clear VMs before run') {
                    script {
                        try{
                            sh '''vagrant destroy load-balancer web-1 web-2 -f
                            sleep 5'''
                        }                
                        catch (e) {
                            echo "No VMs to clear"
                        }
                    }                
                }
            }
        }

        
        stage('Build & Provision VMs') {
            steps {
                sh '''vagrant up
                sleep 10'''
            }
        }

        
        stage('Install docker and deploy containers') {
            steps {
                sh '''cd ansible
                ansible-playbook install-docker.yml
                ansible-playbook install-nginx.yml
                ansible-playbook install-apache1.yml
                ansible-playbook install-apache2.yml'''
            }
        }
        
        
        stage('Web TEST') {
            steps {
                sh '''curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10'''
            }
        }
        

                stage('Destroy used VMs') {
            steps {
                sh 'vagrant destroy load-balancer web-1 web-2 -f'
            }
        } 
    }
}
