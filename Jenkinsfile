pipeline {
    agent any
    environment {
        SLACK_CHANNEL_ID = 'jenkins-ci' // alter if needed, this is default
    }
    stages {
        stage('Ansible Lint Check') {
            steps {
                sh 'ansible-lint -vvvv -x ANSIBLE0010 -x 401 playbooks/*'
            }
        }

        stage('Run Test on Tasks and Inventory Facts') {
            steps {
                sh 'ansible-playbook --syntax-check -i inventory/hosts.yml playbooks/*'
            }
        }
    }

    post {
        always {
            echo "Ansible lint check and playbook syntax test completed."
        }

        success {
            echo "Ansible lint check and playbook syntax test passed successfully."
        }

        failure {
            echo "Ansible lint check or playbook syntax test failed."
        }
    }
}

