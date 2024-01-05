pipeline {
    agent any
    
    environment {
        ANSIBLE_PRIVATE_KEY=credentials('private-key') 
    }

    stages {
        stage('Git-Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dgsuma/Ansible-Jenkins-Nexus-Server-on-AWS-EC2-VM.git'
            }
        }
        
        stage('Ansible') {
            steps {
                sh "ansible --version"
                sh ''' ANSIBLE_SSH_COMMON_ARGS='-o StrictHostKeyChecking=no' ansible -i inventory/hosts server -m ping -u root --private-key=$ANSIBLE_PRIVATE_KEY '''
                
                sh '''ansible-playbook -i inventory/hosts -l server playbooks/nexus.yml -u root --private-key=$ANSIBLE_PRIVATE_KEY -e "ansible_ssh_common_args='-o StrictHostKeyChecking=no'" '''
           
            }
        }
    }
}