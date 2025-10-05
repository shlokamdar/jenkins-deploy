
pipeline {
    agent { label 'flask-demo' }

    stages {
        stage('Install Python and Git') {
            steps {
                sh '''
                    echo "Installing Git and Python..." 
                    sudo yum install -y git
                    sudo yum install -y python3
                    sudo yum install -y python3-pip
                    python3 --version
                    pip3 --version
                    echo "Installation complete!" 
                '''
            }
        }
        stage('Checkout Code'){
            steps{
                checkout scm
                sh "pwd"
            }
        }
        stage('moving the python file')
        steps{
            sh "cp /home/ec2-user/jenkins/workspace/new111 /opt/python-folder/web.py"
        }
    }
}
