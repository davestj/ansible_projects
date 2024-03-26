pipeline {
    agent any
    environment {
        SLACK_CHANNEL_ID = 'jenkins-ci' // alter if needed, this is default
    }
    stages {
	stage('Setup Ansible Build Environment') {
            steps {
                sh 'mkdir -pv logs/;'
            }
        }
        stage('Ansible Validate Variable Definitions') {
            steps {
                sh 'ansible-playbook -vvv -i inventory/hosts.yml playbooks/* --list-tasks'
            }
        }

        stage('Run Test on Tasks and Inventory Facts') {
            steps {
                sh 'ansible-playbook -vvv --syntax-check -i inventory/hosts.yml playbooks/*'
            }
        }
    }

    post {
        always {
            script {
                try {
                    slackSend(channel: env.SLACK_CHANNEL_ID, color: 'good', message: "Ansible lint check and playbook syntax test completed.")
                } catch (Exception e) {
                    echo "Error sending Slack notification: ${e.message}"
                }
            }
        }

        success {
            script {
                try {
                    slackSend(channel: env.SLACK_CHANNEL_ID, color: 'good', message: "Ansible lint check and playbook syntax test passed successfully.")
                } catch (Exception e) {
                    echo "Error sending Slack notification: ${e.message}"
                }
            }
        }

        failure {
            script {
                try {
                    slackSend(channel: env.SLACK_CHANNEL_ID, color: 'danger', message: "Ansible lint check or playbook syntax test failed.")
                } catch (Exception e) {
                    echo "Error sending Slack notification: ${e.message}"
                }
            }
        }
    }
}

