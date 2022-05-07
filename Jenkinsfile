properties([githubProjectProperty(displayName: '', projectUrlStr: 'https://github.com/NoyPhilosof/POC-TEST.git/')])


pipeline {
    agent any

    stages {
        
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'http://github.com/NoyPhilosof/POC-TEST.git'
            }
        }
        
        
        // stage('Create SSH key') {
        //     steps {
        //         sh 'ssh-keygen -f /var/lib/jenkins/.ssh -q -N ""'
        //     }
        // }
       

        stage('Clear Old VMs') {
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

        
        stage('VMs & Provision') {
            steps {
                sh 'vagrant up'
            }
        }
        
        
        stage('wait for VMs') {
            steps {
                sleep 10
            }
        }

        
        stage('Install docker on all VMs') {
            steps {
                sh '''cd ansible
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-docker.yml
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-nginx.yml
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-apache1.yml
                ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-apache2.yml'''
                // sh 'ansible-playbook --private-key=~/.vagrant.d/insecure_private_key -u vagrant -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory install-docker.yml''
                // sh '''cd ansible
                // ansible-playbook ./ansible/install-docker.yml'''
            }
        }
        
        
        // stage('Install nginx + apache') {
        //     steps {
        //         sh '''ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -u vagrant install-nginx.yml
        //         ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -i -u vagrant install-apache1.yml
        //         ansible-playbook --private-key=/var/lib/jenkins/.ssh/id_rsa -i -u vagrant install-apache2.yml'''
        //     }
        // }
        
        
        stage('TEST') {
            steps {
                sh '''curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10
                curl 192.168.80.10'''
            }
        }
        
        
        stage('wait') {
            steps {
                sleep 30
            }
        }           

    
    post {
        always {
            sh 'vagrant destroy -f'
            }
        failure {
            echo "GUESS WHAT???"
            }
        }    
    }
}

