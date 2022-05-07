properties([githubProjectProperty(displayName: '', projectUrlStr: 'https://github.com/NoyPhilosof/POC-TEST.git/')])


pipeline {
    agent any

    stages {
        
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'http://github.com/NoyPhilosof/POC-TEST.git'
            }
        }
        
        
        // stage('Create SSH key') {
        //     steps {
        //         sh 'ssh-keygen -f /var/lib/jenkins/.ssh -q -N ""'
        //     }
        // }
       

        stage('Clean Old VMs') {
            steps {
                catchError(message: 'Clear VMs before run') {
                    script {
                        try{
                            sh '''vagrant destroy -f
                            sleep 10'''
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
                sh 'vagrant up'
            }
        }
        
        
        stage('Give em few more seconds') {
            steps {
                sleep 10
            }
        }

        
        stage('Install docker and deploy containers') {
            steps {
                sh '''cd ansible
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-docker.yml
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-nginx.yml
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-apache1.yml
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-apache2.yml'''
            }
        }
        
        
        stage('Web TEST') {
            steps {
                sh '''curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10'''
            }
        }
        
        
        stage('Few more seconds') {
            steps {
                sleep 30
            }
        }  
        
                stage('Destroy VMs') {
            steps {
                sh 'vagrant destroy -f'
            }
        } 
    }
}
