pipeline {
    agent any

    environment {
        EC2_IP = '18.185.131.125'
    }

    stages {
        stage ('fetch code stage') {
            steps {
                script {
                    echo "Pull source code from Github"
                    git branch: 'main', url: 'https://github.com/ttendaim/jenkins_deploy_ec2.git'
                }
            }
        }
        
        stage ('deploy to EC2') {
            steps {
                script {
                    echo "deploying to shell-script"
                    def shellCmd = "bash ./websetup.sh"
                    sshagent (['ec2-jenkins']) {
                        sh "scp -o StrictHostKeyChecking=no websetup.sh ubuntu@${EC2_IP}:/home/ubuntu"
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@${EC2_IP} ${shellCmd}"
                    }
                }
            }
        }
    }
}
