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

